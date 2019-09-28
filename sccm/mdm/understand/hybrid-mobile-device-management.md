---
title: MDM híbrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Obtenga información sobre la administración híbrida de dispositivos móviles (MDM) con Configuration Manager y Microsoft Intune.
ms.date: 09/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f6c25817973dcfacefe8aae31f0db02dcbd5807
ms.sourcegitcommit: 160bcdaf783f3946ad5c7869b2566cbfc4da545c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401528"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM híbrida con Configuration Manager e Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!WARNING]
> La oferta de servicio de MDM híbrida se retirará a partir del 1 de septiembre de 2019. Los demás dispositivos MDM híbridos no recibirán directivas, aplicaciones ni actualizaciones de seguridad.

## <a name="remove-hybrid-mdm"></a>Quitar MDM híbrida

Si el sitio de Configuration Manager tenía una suscripción de Microsoft Intune, debe quitarlo.

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**. Expanda **Servicios de nube** y seleccione el nodo **Suscripción a Microsoft Intune**. Elimine la suscripción de Intune existente.

1. En el **Asistente para quitar suscripciones de Microsoft Intune**, seleccione la opción para **quitar Microsoft Intune suscripción de Configuration Manager**y, a continuación, haga clic en **siguiente**.

1. Complete el asistente.

## <a name="deprecation-announcement"></a>Anuncio de desuso

La siguiente nota es el anuncio de desuso original:

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). A partir de la versión de servicio 1902 de Intune, prevista para finales de febrero de 2019, los nuevos clientes no pueden crear una conexión híbrida.
> <!--Intune feature 2683117-->  
> Desde que lo lanzamos en Azure hace más de un año, Intune ha agregado cientos de nuevas funcionalidades solicitadas por el cliente y que se encuentran a la vanguardia del sector. Ahora ofrece muchas más funciones que las que hay disponibles a través de la administración híbrida de dispositivos móviles (MDM). Intune en Azure proporciona una experiencia administrativa más integrada y simplificada para sus necesidades de movilidad empresarial.
>
> Como resultado, la mayoría de los clientes eligen Intune en Azure en lugar de MDM híbrida. El número de clientes que usan MDM híbrida sigue disminuyendo a medida que más clientes se trasladan a la nube. Por lo tanto, el 1 de septiembre de 2019 Microsoft retirará la oferta de servicio de MDM híbrida. Planee su [migración a Intune en Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) para satisfacer sus necesidades de MDM.
>
> Este cambio no afecta a Configuration Manager local ni a la [administración conjunta para dispositivos con Windows 10](/sccm/comanage/overview). Si no está seguro de si está utilizado MDM híbrida,vaya al área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y haga clic en **Suscripciones a Microsoft Intune**. Si tiene una suscripción a Microsoft Intune configurada, el inquilino está configurado para MDM híbrida.
>
> **¿Cómo me afecta esto a mí?**
>
> - Microsoft seguirá permitiendo el uso de MDM híbrida durante el próximo año. La característica continuará recibiendo importantes correcciones de errores. Microsoft brindará soporte a la funcionalidad existente en nuevas versiones de sistemas operativos, como la inscripción en iOS 12. No habrá ninguna característica nueva para MDM híbrida.  
>
> - Si migra a Intune en Azure antes del final de la oferta de MDM híbrida, el usuario final no debería notar nada.  
>
> - El 1 de septiembre de 2019, los dispositivos de MDM híbrida que queden ya no recibirán directivas, aplicaciones ni actualizaciones de seguridad.  
>
> - Las licencias siguen siendo las mismas. Las licencias de Intune en Azure se incluyen con MDM híbrida.  
>
> - La característica MDM local de Configuration Manager no está en desuso. A partir de Configuration Manager versión 1810, puede usar MDM local sin una conexión de Intune. Para obtener más información, consulte ya [no se necesita una conexión de Intune para las nuevas implementaciones de MDM local](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm).
>
> - La característica de acceso condicional local de Configuration Manager también está en desuso con MDM híbrida. Si usa el acceso condicional en dispositivos administrados con el cliente de Configuration Manager, asegúrese de que estén protegidos antes de migrar.
>     1. Configuración de directivas de acceso condicional en Azure
>     2. Configuración de directivas de cumplimiento en el portal de Intune
>     3. Finalizar la migración híbrida y establecer la entidad de MDM en Intune
>     4. Habilitación de la administración conjunta
>     5. Traslado de la carga de trabajo de administración conjunta de directivas de cumplimiento a Intune
>
>     Para obtener más información, consulte [acceso condicional con administración conjunta](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access).
>
> **¿Qué he de hacer para prepararme para este cambio?**
>
> - Comience a planear la migración de MDM desde la consola de Configuration Manager a Azure. Muchos clientes, incluidos los informáticos de Microsoft, han llevado a cabo este proceso. Para obtener más información, consulte este [caso práctico de Microsoft](https://aka.ms/Intune_MSFT).  
>
> - Revise las siguientes herramientas y documentación para simplificar el proceso de migración de MDM híbrida a Intune en Azure:  
>   - [Importar datos de Configuration Manager a Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>   - [Migración de dispositivos y usuarios de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
>
> - Póngase en contacto con su socio de registro o FastTrack para obtener ayuda. [FastTrack para Microsoft 365](https://aka.ms/hybrid_fasttrack) puede ayudar en la migración de MDM híbrida a Intune en Azure.
>
> Para obtener más información, vea la [entrada del blog de soporte técnico de Intune](https://aka.ms/hybrid_notification).

<!--

With the hybrid mobile device management (MDM) feature of Configuration Manager, manage iOS, Windows, and Android devices. All management tasks are handled from the Configuration Manager console where you perform the rest of your management tasks seamlessly integrated with Microsoft Intune's online service over the internet. Use Configuration Manager to let users access company resources on their devices in a secure, managed way. By using device management, you protect company data while letting users enroll their personal or company-owned devices to access company data. 

This article assumes that you use Configuration Manager to manage computers. It also assumes that you're interested in extending the Configuration Manager console with Intune to manage mobile devices. 



## Capabilities

Hybrid MDM supports the following management capabilities on devices:

-   Retire and wipe devices  

-   Configure compliance settings such as passwords, security, roaming, encryption, and wireless communication  

-   Deploy line-of-business (LOB) apps to devices  

-   Deploy apps to devices that connect to Windows Store, Windows Phone Store, App Store, or Google Play  

-   Collect hardware inventory  

-   Collect software inventory by using built-in reports  



## Hybrid MDM enrollment

To bring devices into hybrid management, those devices must be enrolled with the service. How devices enroll devices depends on the device type, ownership, and the level of management needed.

- **"Bring your own device" (BYOD)**: Users enroll their personal phones, tablets, or PCs  

- **Corporate-owned device (COD)**: Enable management scenarios like remote wipe, shared devices, or user affinity for a device  

- If you use [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), either on-premises or hosted in the cloud, you can enable simple Intune management without enrollment. Windows PCs can also be managed using [Intune client software](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

-->

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre las características admitidas para administrar dispositivos MDM, consulte los siguientes artículos:

- [¿Qué es Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [¿Qué es MDM local?](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure)
- [Administración de dispositivos con Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync)
