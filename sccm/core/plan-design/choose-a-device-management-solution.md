---
title: 'Elegir una solución de administración de dispositivos '
titleSuffix: Configuration Manager
description: Obtenga información sobre las soluciones que ofrece System Center Configuration Manager para administrar equipos, servidores y dispositivos.
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a520e4e43ca2d7de080272c213c5768cbd284501
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415847"
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Elegir una solución de administración de dispositivos para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

System Center Configuration Manager (también conocido como ConfgMgr o SCCM) ofrece diferentes soluciones para la administración de equipos, servidores y dispositivos. Puede elegir la solución adecuada en función de las plataformas de dispositivos que necesita administrar y la funcionalidad de administración que necesita.  


##  <a name="overview-of-device-management-solutions"></a>Información general sobre las soluciones de administración de dispositivos  
 En este artículo se describen cuatro soluciones de administración de dispositivos: la aplicación cliente de Configuration Manager, la infraestructura local de Configuration Manager, Microsoft Intune y Exchange. El artículo finaliza con dos tablas en las que se comparan las soluciones de administración, una según las [plataformas de dispositivos móviles compatibles](#compare-device-management-solutions-based-on-supported-mobile-device-platforms) y la otra según la [funcionalidad de administración](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Administrar dispositivos con el cliente de Configuration Manager  

Esta opción, que necesita la instalación de la aplicación cliente de Configuration Manager en los dispositivos, es la que proporciona más características para administrar equipos, servidores y otros dispositivos en el entorno. Para más información, consulte [Métodos de instalación de cliente en System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Administrar dispositivos con la infraestructura local de Configuration Manager  

Esta opción usa las funcionalidades de administración de dispositivos integradas en los sistemas operativos de algunas plataformas de dispositivos. Aunque no incluye tantas características como la administración basada en cliente, la administración local de dispositivos móviles proporciona un enfoque más ligero para la administración, mediante recursos locales de Configuration Manager para conectarse a los dispositivos y administrarlos. Tenga en cuenta que esta opción solo se admite actualmente para equipos de Windows 10 y dispositivos de Windows 10 Mobile.  

Para obtener más información, consulte este artículo sobre cómo [administrar dispositivos móviles con la infraestructura local en System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Administrar dispositivos con Microsoft Intune (híbrido)  

Esta opción usa Microsoft Intune para inscribir y administrar dispositivos, en lugar de emplear los recursos locales de Configuration Manager. Aunque Intune administra los dispositivos, se puede tener acceso a las tareas de administración en la consola de Configuration Manager. Esta opción es compatible con todos los sistemas operativos principales de dispositivos móviles, incluidos Windows 10 Mobile, Windows Phone, iOS, Mac OS X y Android. También proporciona administración de equipos de Windows 8.1 y Windows 10 en su organización.  

Para obtener más información, consulte [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md) (Administración híbrida de dispositivos móviles [MDM] con System Center Configuration Manager y Microsoft Intune)  

###  <a name="manage-devices-with-microsoft-exchange"></a>Administrar dispositivos con Microsoft Exchange  

Esta opción usa el conector de Exchange Server para conectar varios servidores de Exchange con Configuration Manager. De este modo se centraliza la administración de los dispositivos que pueden conectarse a Exchange ActiveSync. Puede configurar las características de administración de dispositivos móviles de Exchange, como la eliminación remota de datos del dispositivo móvil y el control de configuración para varios servidores de Exchange, desde la consola de Configuration Manager.  

Para más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Puede usar las soluciones de administración de dispositivos por sí solas o en combinación con otras. Por ejemplo, puede usar el enfoque de administración basada en cliente para administrar los equipos y los servidores de la organización y, además, usar Intune para administrar los dispositivos móviles. Al combinar los enfoques de esta manera, puede cubrir todas las necesidades de administración del dispositivo desde la consola de Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Comparar soluciones de administración de dispositivos basadas en plataformas de dispositivos móviles compatibles  

|Plataforma|Con el cliente de Configuration Manager|Configuration Manager con Microsoft Intune (híbrida)|Administración local de dispositivos móviles|Configuration Manager con Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Sí||Sí|  
|iOS||Sí||Sí|  
|Mac OS X|Sí|||Sí|  
|UNIX/Linux|Sí|||Sí|  
|Windows 10|Sí|Sí|Sí|Sí|  
|Windows 10 Mobile||Sí|Sí|Sí|  
|Windows (versiones anteriores)|Sí|Sí||Sí|  
|Windows CE|Sí (con cliente heredado de dispositivo móvil)|||Sí|  
|Windows Embedded|Sí||||  
|Windows Phone||Sí||Sí|  
|Windows Server|Sí|||Sí|  

 Para obtener una lista completa de las plataformas compatibles, vea [Supported operating systems for clients and devices for System Center Configuration Manager (Sistemas operativos compatibles con clientes y dispositivos para System Center Configuration Manager)](configs/supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Comparar soluciones de administración de dispositivos móviles basadas en la funcionalidad de administración  

|Funcionalidad de administración|Con el cliente de Configuration Manager|Configuration Manager con Microsoft Intune (híbrida)|Administración local de dispositivos móviles|Configuration Manager con Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Seguridad de infraestructura de clave pública (PKI) entre el dispositivo móvil y Configuration Manager (usa la autenticación mutua y SSL para cifrar las transferencias de datos)|Sí|Sí|Sí||  
|Instalación de cliente|Sí||||  
|Soporte técnico a través de Internet|Sí||||  
|Detección|Sí|||Sí|  
|Inventario de hardware|Sí|Sí|Sí|Sí|  
|Inventario de software|Sí|||Sí|  
|Configuración|Sí|Sí|Sí|Sí|  
|Implementación de software|Sí|Sí|Sí||  
|Supervisar con punto de estado de reserva|Sí||||  
|Conexiones a puntos de administración|Sí||Sí||  
|Conexiones a puntos de distribución|Sí||Sí||  
|Bloqueo desde Configuration Manager|Sí|Sí|Sí||  
|Cuarentena y bloqueo desde Exchange Server (y Configuration Manager)||||Sí|  
|Borrado remoto| |Sí|Sí|Sí|  
