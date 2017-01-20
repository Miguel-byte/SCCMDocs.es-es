---
title: Requisitos previos del control remoto | System Center Configuration Manager
description: Cumpla los requisitos previos del control remoto en System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1b2057e-b74f-43fa-a293-763a8f866d3d
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5e15fc7359787b40ebd138fd79dd72081dd8fb36


---
# <a name="prerequisites-for-remote-control-in-system-center-configuration-manager"></a>Requisitos previos del control remoto en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

El control remoto de System Center Configuration Manager tiene dependencias externas y dependencias dentro del producto.  

## <a name="dependencies-external-to-configuration-manager"></a>Dependencias externas a Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|Controlador de tarjeta de vídeo del equipo|Asegúrese de que el controlador de vídeo más reciente esté instalado en los equipos cliente para garantizar un rendimiento óptimo del control remoto.|  

 Los dispositivos que ejecutan Windows Embedded, Windows Embedded para punto de servicio (POS) y Windows Fundamentals for Legacy PCs no admiten el visor de control remoto, pero admiten el cliente de control remoto.  

 El control remoto de Configuration Manager no se puede usar para administrar de forma remota los equipos cliente que ejecuten Systems Management Server 2003 o Configuration Manager 2007.  

> [!NOTE]  
>  No se requieren servicios de Windows como una dependencia externa para el control remoto.  

### <a name="supported-operating-systems-for-the-remote-control-viewer"></a>Sistemas operativos compatibles con el visor de control remoto  
 En la tabla siguiente se ofrece información sobre los sistemas operativos compatibles con el visor de control remoto. Para obtener información sobre los sistemas operativos cliente compatibles, consulte [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md) (Configuraciones admitidas para System Center Configuration Manager).  

|Sistema operativo|Compatibilidad con el visor|Más información|  
|----------------------|--------------------|----------------------|  
|Windows XP (32 bits)|Sí|Para ejecutar el visor de control remoto en este sistema operativo, primero debe descargar e instalar la [Actualización del cliente de Conexión a Escritorio remoto (RDC) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) en el Centro de descarga de Microsoft.|  
|Windows XP (64 bits)|No|No hay información adicional.|  
|Windows Vista (32 bits)|Sí|Para ejecutar el visor de control remoto en este sistema operativo, primero debe descargar e instalar la [Actualización del cliente de Conexión a Escritorio remoto (RDC) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) en el Centro de descarga de Microsoft.|  
|Windows Vista (64 bits)|Sí|Para ejecutar el visor de control remoto en este sistema operativo, primero debe descargar e instalar la [Actualización del cliente de Conexión a Escritorio remoto (RDC) 7.0 (KB969084)](https://www.microsoft.com/en-us/download/details.aspx?id=12767) en el Centro de descarga de Microsoft.|  
|Windows 7 (32 bits)|Sí|No hay información adicional.|  
|Windows 7 (64 bits)|Sí|No hay información adicional.|  
|Windows Server 2003 (32 bits)|No|No hay información adicional.|  
|Windows Server 2003 (64 bits)|No|No hay información adicional.|  
|Windows Server 2008 (32 bits)|No|No hay información adicional.|  
|Windows Server 2008 (64 bits)|No|No hay información adicional.|  
|Windows Server 2008 R2 (64 bits)|Sí|No hay información adicional.|  

## <a name="configuration-manager-dependencies"></a>Dependencias de Configuration Manager  

|Dependencia|Más información|  
|----------------|----------------------|  
|El control remoto debe habilitarse para los clientes|De forma predeterminada, el control remoto no está habilitado cuando se instala Configuration Manager. Para obtener información sobre cómo habilitar y configurar el control remoto, consulte [Configuración del control remoto en System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).|  
|Puede configurar otras fuentes de actualización opcionales si crea una directiva antimalware.|El rol de sistema de sitio de punto de servicios de informes debe instalarse antes de poder ejecutar informes para el control remoto. Para obtener más información, consulte [Generación de informes en System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Permisos de seguridad para administrar el control remoto|Para acceder a recursos de la recopilación e iniciar una sesión de control remoto desde la consola de Configuration Manager: permisos **Controlar AMT**, **Leer**, **Leer recurso** y **Control remoto** para el objeto **Recopilación**.<br /><br /> El rol de seguridad **Operador de herramientas remotas** incluye estos permisos, que son necesarios para administrar el control remoto en Configuration Manager.<br /><br /> Para obtener más información, consulte [Configurar la administración basada en roles de System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).<br /><br /> Además, debe agregar usuarios a los que quiera conceder permiso para utilizar el control remoto y la asistencia remota a la lista de vistas permitidas de control remoto mediante la opción **Visores permitidos de control remoto y asistencia remota** en la configuración de cliente **Herramientas remotas** .|  



<!--HONumber=Nov16_HO1-->


