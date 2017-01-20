---
title: "Elegir una solución de administración de dispositivos para System Center Configuration Manager"
description: "Obtenga información sobre las soluciones que ofrece System Center Configuration Manager para administrar equipos, servidores y dispositivos."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Elegir una solución de administración de dispositivos para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager ofrece diferentes soluciones para la administración de equipos, servidores y dispositivos. Puede elegir la solución adecuada en función de las plataformas de dispositivos que necesita administrar y la funcionalidad de administración que necesita.  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> Información general sobre las soluciones de administración de dispositivos  
 Las siguientes opciones están disponibles para administrar equipos y dispositivos con Configuration Manager:  

-   **Administración de dispositivos con el cliente de Configuration Manager**  

     Esta opción, que necesita la instalación de la aplicación de cliente de Configuration Manager en cada dispositivo que se va a administrar, es la que proporciona más características y funcionalidad para administrar equipos, servidores y otros dispositivos en el entorno. Esta opción es la forma tradicional en que Configuration Manager ha proporcionado la administración de dispositivos en el pasado.  

     Para más información sobre esta solución, vea [Client installation methods in System Center Configuration Manager (Métodos de instalación de cliente en System Center Configuration Manager)](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Administración de dispositivos móviles con la infraestructura local de Configuration Manager**  

     Esta opción usa las funcionalidades de administración de dispositivos integradas en los sistemas operativos de determinadas plataformas de dispositivos. Aunque no incluye tantas características como la administración basada en cliente, la administración local de dispositivos móviles proporciona un enfoque más ligero para la administración, que usa recursos de Configuration Manager locales para conectarse a los dispositivos y administrarlos. La administración local de dispositivos móviles solo se admite de momento en equipos y dispositivos móviles de Windows 10.  

     Para más información sobre esta solución, vea [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager (Administrar dispositivos móviles con la infraestructura local de System Center Configuration Manager)](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

-   **Administración de dispositivos móviles con Microsoft Intune (híbrida)**  

     Esta opción se conoce como administración híbrida de dispositivos móviles.  Usa Microsoft Intune para inscribir y administrar dispositivos en lugar de emplear los recursos locales de Configuration Manager. Aunque Intune administra los dispositivos, el usuario controla las tareas de administración en la consola de Configuration Manager. Esta opción es compatible con todos los sistemas operativos principales de dispositivos móviles, incluidos Windows 10 Mobile, Windows Phone, iOS y Android. También proporciona administración de equipos de Windows 8.1 y Windows 10 en su organización.  

     Para más información sobre esta solución, vea [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune (Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune)](../../mdm/plan-design/hybrid-mobile-device-management.md).  

-   **Administración de dispositivos móviles con Exchange**  

     Esta opción, que usa el conector de Exchange Server para conectar varios servidores de Exchange a Configuration Manager, centraliza la administración de los dispositivos que se pueden conectar a Exchange ActiveSync. Puede configurar las características de administración de dispositivos móviles de Exchange, como la eliminación remota de datos del dispositivo móvil y el control de configuración para varios servidores de Exchange, desde la consola de Configuration Manager.  

     Para más información sobre esta solución, vea [Manage mobile devices with System Center Configuration Manager and Exchange (Administrar dispositivos móviles con System Center Configuration Manager y Exchange)](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)  

 Puede usar las soluciones de administración de dispositivos por sí solas o en combinación con otras. Por ejemplo, puede usar el enfoque de administración basada en cliente para la administración de los equipos y los servidores de la organización y, además, usar la administración basada en Intune para los dispositivos móviles. Al combinar los enfoques de esta manera, puede cubrir todas las necesidades de administración del dispositivo y controlarlo todo desde la consola de Configuration Manager.  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> Comparar soluciones de administración de dispositivos basadas en plataformas de dispositivos móviles compatibles  

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

 Para obtener una lista completa de las plataformas compatibles, vea [Supported operating systems for clients and devices for System Center Configuration Manager (Sistemas operativos compatibles con clientes y dispositivos para System Center Configuration Manager)](configs\supported-operating-systems-for-clients-and-devices.md).

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> Comparar soluciones de administración de dispositivos móviles basadas en la funcionalidad de administración  

|Funcionalidad de administración|Con el cliente de Configuration Manager|Configuration Manager con Microsoft Intune (híbrida)|Administración local de dispositivos móviles|Configuration Manager con Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Seguridad de infraestructura de clave pública (PKI) entre el dispositivo móvil y Configuration Manager mediante la autenticación mutua y SSL para cifrar las transferencias de datos|Sí|Sí|Sí||  
|Instalación de cliente|Sí||||  
|Soporte técnico a través de Internet|Sí||||  
|Detección|Sí|||Sí|  
|Inventario de hardware|Sí|Sí|Sí|Sí|  
|Inventario de software|Sí|||Sí|  
|Configuración|Sí|Sí|Sí|Sí|  
|Implementación de software|Sí|Sí|Sí||  
|Supervisar con punto de estado de reserva|Sí||||  
|Conexiones a puntos de administración|Sí||Sí||  
|Conexiones a puntos de distribución|Sí|Sí|Sí||  
|Bloqueo desde Configuration Manager|Sí|Sí|Sí||  
|Cuarentena y bloqueo desde Exchange Server (y Configuration Manager)||||Sí|  
|Borrado remoto|Sí|Sí|Sí|Sí|  



<!--HONumber=Nov16_HO1-->


