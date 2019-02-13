---
title: MDM híbrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Obtenga información sobre la administración híbrida de dispositivos móviles (MDM) con Configuration Manager y Microsoft Intune.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2980cef8a39f790dbb94ab85fa025eeb04f4f996
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139296"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM híbrida con Configuration Manager e Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). A partir de la versión del servicio Intune 1902, que se esperaba el final de febrero de 2019, los clientes nuevos no pueden crear una nueva conexión híbrida. 
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
> - La característica MDM local en Configuration Manager no está en desuso. A partir de la versión de Configuration Manager 1810, puede usar MDM local sin conexión a Intune. Para obtener más información, consulte [Intune una conexión ya no es necesario para nuevas implementaciones de MDM local](/sccm/core/plan-design/changes/whats-new-in-version-1810#bkmk_opmdm). 
> 
> - La característica de acceso condicional en el entorno local de Configuration Manager también está en desuso con MDM híbrida. Si usa acceso condicional en los dispositivos administrados con el cliente de Configuration Manager, asegúrese de que están protegidos antes de migrar. 
>     1. Configurar directivas de acceso condicional en Azure
>     2. Configurar directivas de cumplimiento en el portal de Intune 
>     3. Finalizar la migración híbrida y establecer la entidad de MDM en Intune
>     4. Habilitación de la administración conjunta
>     5. Mover la carga de trabajo de administración conjunta de las directivas de cumplimiento a Intune 
>
>     Para obtener más información, consulte [el acceso condicional con administración conjunta](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 
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

- **"Bring your own device" (BYOD)**: Los usuarios inscribir sus teléfonos personales, tabletas o equipos  

- **Dispositivos corporativos (COD)**: Habilitar escenarios de administración como el borrado remoto, dispositivos compartidos o afinidad de usuario para un dispositivo  

- Si usa [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager), de manera local u hospedado en la nube, puede habilitar la administración simple de Intune sin la inscripción. Los equipos con Windows también pueden administrarse mediante el [software cliente de Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
