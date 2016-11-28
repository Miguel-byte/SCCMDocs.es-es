---
title: Configurar Endpoint Protection | System Center Configuration Manager
description: Aprenda a administrar la seguridad y el malware en equipos cliente de System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5905ab3f63a9956909f3d26136a377ca2f65b71c


---
# <a name="configuring-endpoint-protection-in-system-center-configuration-manager"></a>Configurar Endpoint Protection en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Para usar Endpoint Protection para administrar la seguridad y el malware en equipos cliente de Configuration Manager, configúrelo según las instrucciones de este tema.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Cómo configurar Endpoint Protection en Configuration Manager  
 Endpoint Protection en Configuration Manager tiene dependencias dentro y fuera del producto.  

### <a name="configure-endpoint-protection-in-configuration-manager"></a>Configurar Endpoint Protection en Configuration Manager  
Hay cinco pasos para configurar Endpoint Protection:

|Paso|Detalles|
|---|----|
|Paso 1|[Crear un rol de sistema de sitio de punto de Endpoint Protection](endpoint-protection-site-role.md): instale el rol de sistema de sitio de punto de Endpoint Protection. |
|Paso 2|[Configurar alertas para Endpoint Protection](endpoint-configure-alerts.md): configure alertas de Endpoint Protection para notificar a los administradores cuando se produzcan eventos de seguridad concretos en la jerarquía.|
|Paso 3 | [Configurar orígenes de actualización de definiciones para los clientes de Endpoint Protection](endpoint-definition-updates.md): elija entre los métodos disponibles para mantener actualizadas las definiciones de antimalware en los equipos cliente.|
|Paso 4|[Configurar la directiva antimalware predeterminada y crear directivas antimalware personalizadas](endpoint-antimalware-policies.md): la directiva antimalware predeterminada se aplica al instalar el cliente de Endpoint Protection; las directivas personalizadas se aplican a los 60 minutos de la implementación del cliente.|
|Paso 5|[Configurar las opciones de cliente personalizadas de Endpoint Protection](endpoint-protection-configure-client.md): configure las opciones de cliente personalizadas de Endpoint Protection para implementar en las colecciones de equipos.|

> [!IMPORTANT]  
>  Si administra Endpoint Protection para equipos con Windows 10, debe configurar Configuration Manager para actualizar y distribuir las definiciones de malware de Windows Defender. Windows Defender se incluye en Windows 10, pero todavía se tiene que instalar SCEPInstall y aún se necesita la configuración de cliente personalizada de Endpoint Protection (paso 5).  



<!--HONumber=Nov16_HO1-->


