---
title: MDM híbrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Obtenga información sobre la administración híbrida de dispositivos móviles (MDM) con Configuration Manager y Microsoft Intune.
ms.date: 11/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f3d25120701c12b547727259002fc58a8f8f0780
ms.sourcegitcommit: 97083c51057e2c4e0fe12c3b1f1b512250874c6a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2018
ms.locfileid: "50968142"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM híbrida con Configuration Manager e Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
> <!--Intune feature 2683117-->  
> Desde que lo lanzamos en Azure hace más de un año, Intune ha agregado cientos de nuevas funcionalidades solicitadas por el cliente y que se encuentran a la vanguardia del sector. Ahora ofrece muchas más funciones que las que hay disponibles a través de la administración híbrida de dispositivos móviles (MDM). Intune en Azure proporciona una experiencia administrativa más integrada y simplificada para sus necesidades de movilidad empresarial.
> 
> Como resultado, la mayoría de los clientes eligen Intune en Azure en lugar de MDM híbrida. El número de clientes que usan MDM híbrida sigue disminuyendo a medida que más clientes se trasladan a la nube. Por lo tanto, el 1 de septiembre de 2019 Microsoft retirará la oferta de servicio de MDM híbrida. Planee su [migración a Intune en Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) para satisfacer sus necesidades de MDM. 
> 
> Este cambio no afecta a Configuration Manager local ni a la [administración conjunta para dispositivos con Windows 10](/sccm/core/clients/manage/co-management-overview). Si no está seguro de si está utilizado MDM híbrida,vaya al área de trabajo **Administración** de la consola de Configuration Manager, expanda **Servicios de nube** y haga clic en **Suscripciones a Microsoft Intune**. Si tiene una suscripción a Microsoft Intune configurada, el inquilino está configurado para MDM híbrida.
> 
> **¿Cómo me afecta esto a mí?**
> 
> - Microsoft seguirá permitiendo el uso de MDM híbrida durante el próximo año. La característica continuará recibiendo importantes correcciones de errores. Microsoft brindará soporte a la funcionalidad existente en nuevas versiones de sistemas operativos, como la inscripción en iOS 12. No habrá ninguna característica nueva para MDM híbrida.  
> 
> - Si migra a Intune en Azure antes del final de la oferta de MDM híbrida, el usuario final no debería notar nada.  
> 
> - Las licencias siguen siendo las mismas. Las licencias de Intune en Azure se incluyen con MDM híbrida.  
> 
> - Las características de MDM local y de acceso condicional de Configuration Manager no están en desuso. Los próximos cambios en Configuration Manager permitirán que estas características funcionen sin MDM híbrida. 
> 
> - El 1 de septiembre de 2019, los dispositivos de MDM híbrida que queden ya no recibirán directivas, aplicaciones ni actualizaciones de seguridad.  
> 
> **¿Qué he de hacer para prepararme para este cambio?**
> 
> - Comience a planear la migración de MDM desde la consola de Configuration Manager a Azure. Muchos clientes, incluidos los informáticos de Microsoft, han llevado a cabo este proceso. Para obtener más información, consulte este [caso práctico de Microsoft](https://aka.ms/Intune_MSFT).  
> 
> - Revise las siguientes herramientas y documentación para simplificar el proceso de migración de MDM híbrida a Intune en Azure:  
>     - [Importar datos de Configuration Manager a Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Migración de dispositivos y usuarios de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Póngase en contacto con su socio de registro o FastTrack para obtener ayuda. [FastTrack para Microsoft 365](https://aka.ms/hybrid_fasttrack) puede ayudar en la migración de MDM híbrida a Intune en Azure. 
> 
> Para obtener más información, vea la [entrada del blog de soporte técnico de Intune](https://aka.ms/hybrid_notification).



Con la característica de administración híbrida de dispositivos móviles (MDM) de Configuration Manager, administre dispositivos Android, iOS y Windows. Todas las tareas de administración se controlan desde la consola de Configuration Manager donde realiza el resto de las tareas de administración que se integran perfectamente al servicio en línea de Microsoft Intune mediante Internet. Use Configuration Manager para permitir a los usuarios un acceso seguro y administrado a los recursos de la compañía en sus dispositivos. Mediante el uso de la administración de dispositivos, se protegen los datos de la compañía a la vez que se permite a los usuarios inscribir sus dispositivos corporativos o personales para tener acceso a los datos de la compañía. 

En este artículo se da por supuesto que usa Configuration Manager para administrar equipos. También se da por supuesto que está interesado en la ampliación de la consola de Configuration Manager con Intune para administrar dispositivos móviles. 



## <a name="capabilities"></a>Capacidades

MDM híbrida admite las siguientes capacidades de administración en los dispositivos:

-   Retirar y borrar dispositivos  

-   Definir la configuración de cumplimiento, como contraseñas, seguridad, movilidad, cifrado y comunicación inalámbrica  

-   Implementar aplicaciones de línea de negocio (LOB) en los dispositivos  

-   Implementar aplicaciones en los dispositivos que se conectan a la Tienda Windows, la Tienda Windows Phone, App Store o Google Play  

-   Recopilar información de inventario de hardware  

-   Recopilar información de inventario de software mediante el uso de informes integrados  

Para leer sobre las nuevas características que están disponibles para MDM híbrido, consulte [What's new in hybrid mobile device management (Novedades en la administración híbrida de dispositivos móviles)](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management).



## <a name="hybrid-mdm-enrollment"></a>Inscripción híbrida de MDM

Para integrar dispositivos en la administración híbrida, esos dispositivos deben inscribirse al servicio. La manera en que los dispositivos inscriben dispositivos depende del tipo de dispositivo, la propiedad y el nivel de administración necesario.

- **"Bring Your Own Device" (BYOD)**: los usuarios inscriben sus teléfonos personales, tabletas o PC.  

- **Dispositivo de propiedad corporativa (COD)**: habilite la administración de escenarios como el borrado remoto, los dispositivos compartidos o la afinidad de usuario para un dispositivo.  

- Si usa [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), de manera local u hospedado en la nube, puede habilitar la administración simple de Intune sin la inscripción. Los equipos con Windows también pueden administrarse mediante el [software cliente de Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
