---
title: Elegir una solución de administración de dispositivos
titleSuffix: Configuration Manager
description: Obtenga información sobre las soluciones que ofrece Configuration Manager para administrar equipos, servidores y dispositivos.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1aec1447207d20393b0b8454851755ec85f5020
ms.sourcegitcommit: abfc9e1b3945637fa93ca8d3a11519493a5d5391
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66264362"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Elección de una solución de administración de dispositivos para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager ofrece diferentes soluciones para la administración de equipos, servidores y dispositivos. Elija la solución más adecuada para la organización en función de su decisión sobre las plataformas de dispositivos que necesita administrar y la funcionalidad de administración que necesita.  


> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>Información general

En este artículo se tratan las cuatro soluciones siguientes de administración de dispositivos: 
- [Cliente de Configuration Manager](#bkmk_sccm)
- [Administración de dispositivos móviles (MDM) local con Configuration Manager](#bkmk_opmdm)
- [Administración conjunta con Microsoft Intune](#bkmk_comanage)
- [Microsoft Exchange](#bkmk_opmdm)

Puede usar las soluciones de administración de dispositivos por sí solas o en combinación con otras. Por ejemplo, puede usar el enfoque de administración basada en cliente para administrar los equipos y los servidores de la organización y, además, usar la administración conjunta para administrar equipos portátiles basados en Internet. Al combinar los enfoques de esta manera, puede cubrir todas las necesidades de administración del dispositivo.  

El artículo también incluye dos tablas que comparan las soluciones de administración por los siguientes factores: 
- [Comparación por plataformas admitidas](#bkmk_comp1)
- [Comparación por funcionalidad de administración](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Cliente de Configuration Manager  

Esta opción requiere la instalación del cliente de Configuration Manager en dispositivos. Proporciona la mayoría de las características para administrar equipos, servidores y otros dispositivos del entorno. 

Para obtener más información, vea [Métodos de instalación de cliente en System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> MDM local  

Esta opción usa las funcionalidades de administración de dispositivos integradas en Windows 10. Aunque no incluye tantas características como la administración basada en cliente, la administración de dispositivos móviles locales proporciona un enfoque más ligero para la administración. Usa recursos locales de Configuration Manager para administrar dispositivos.  

Para obtener más información, consulte [Administrar dispositivos móviles con la infraestructura local](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a> Administración conjunta con Microsoft Intune

La administración conjunta es una de las principales formas de asociar la implementación existente de Configuration Manager a la nube de Microsoft 365. Le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune. La administración conjunta le permite asociar a la nube su inversión existente en Configuration Manager mediante la incorporación de nuevas funcionalidades. 

Para más información, vea [What is co-management?](/sccm/comanage/overview) (¿Qué es la administración conjunta?).  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

Esta opción usa el conector de Exchange Server para conectar varios servidores de Exchange con Configuration Manager. De este modo se centraliza la administración de los dispositivos que pueden conectarse a Exchange ActiveSync. Puede configurar características de administración de dispositivos móviles de Exchange desde la consola de Configuration Manager. Entre las características de ejemplo se incluyen el borrado remoto de dispositivos y el control de configuración para varios servidores de Exchange.

Para obtener más información, consulte [Administrar dispositivos móviles mediante System Center Configuration Manager y Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Comparación de soluciones por plataformas admitidas  

|Plataforma|Cliente de Configuration Manager|MDM local|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Sí|  
|iOS| | |Sí|  
|Mac OS X|Sí| |Sí|  
|UNIX/Linux|Sí| |Sí|  
|Windows 10|Sí|Sí|Sí|  
|Windows 10 Mobile| |Sí|Sí|  
|Windows (versiones anteriores)|Sí| |Sí|  
|Windows Server|Sí| |Sí|  
|Windows CE|Sí (con cliente heredado de dispositivo móvil)| |Sí|  
|Windows Embedded|Sí| | |  
|Windows Mobile| | |Sí|  

Para obtener una lista completa de las plataformas compatibles, vea [Supported operating systems for clients and devices for System Center Configuration Manager (Sistemas operativos compatibles con clientes y dispositivos para System Center Configuration Manager)](configs/supported-operating-systems-for-clients-and-devices.md).

Microsoft recomienda usar Intune para administrar dispositivos móviles Android, iOS y Windows 10. Para más información, consulte [¿Qué es Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune).



##  <a name="bkmk_comp2"></a> Comparación de soluciones por funcionalidad de administración  

|Funcionalidad de administración|Cliente de Configuration Manager|MDM local|Configuration Manager con Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Seguridad de infraestructura de clave pública (PKI) entre el dispositivo móvil y Configuration Manager (usa la autenticación mutua y SSL para cifrar las transferencias de datos)|Sí|Sí| |  
|Instalación de cliente|Sí| | |  
|Soporte técnico a través de Internet|Sí| | |  
|Detección|Sí| |Sí|  
|Inventario de hardware|Sí|Sí|Sí|  
|Inventario de software|Sí| |Sí|  
|Configuración|Sí|Sí|Sí|  
|Implementación de software|Sí|Sí| |  
|Supervisar con punto de estado de reserva|Sí| | |  
|Conexiones a puntos de administración|Sí|Sí| |  
|Conexiones a puntos de distribución|Sí|Sí| |  
|Bloqueo desde Configuration Manager|Sí|Sí| |  
|Cuarentena y bloqueo desde Exchange Server (y Configuration Manager)| | |Sí|  
|Borrado remoto| |Sí|Sí|  


