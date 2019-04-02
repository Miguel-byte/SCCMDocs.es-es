---
title: Administración conjunta de cargas de trabajo
titleSuffix: Configuration Manager
description: Obtenga información sobre las cargas de trabajo que puede cambiar de Configuration Manager a Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3723595091e57a7ad2267a4da325e7c134c7bf1
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "56755553"
---
# <a name="co-management-workloads"></a>Administración conjunta de cargas de trabajo

No es necesario que cambie las cargas de trabajo o puede cambiarlas individualmente cuando esté preparado. Configuration Manager sigue administrando todas las demás cargas de trabajo, incluidas las que no cambia a Intune, y todas las demás características de Configuration Manager que no admite la administración conjunta.

La administración conjunta admite estas cargas de trabajo:

- [Directivas de cumplimiento](#compliance-policies)  

- [Directivas de Windows Update](#windows-update-policies)  

- [Directivas de acceso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuración del dispositivo](#device-configuration)  

- [Aplicaciones de Office para hacer clic y ejecutar](#office-click-to-run-apps)  

- [Aplicaciones cliente](#client-apps)  



## <a name="compliance-policies"></a>Directivas de cumplimiento 

Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. 

Para más información sobre la característica de Intune, consulte [Directivas de cumplimiento de dispositivos](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Directivas de Windows Update

Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. 

Para más información sobre la característica de Intune, consulte [Configuración de directivas de aplazamiento de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Directivas de acceso a recursos

Las directivas de acceso a recursos configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos. 

Para más información sobre la característica de Intune, consulte el artículo sobre cómo [implementar perfiles de acceso a recursos](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

A partir de Configuration Manager 1802, la carga de trabajo de Endpoint Protection incluye el conjunto de características de protección antimalware de Windows Defender: 

- Protección de aplicaciones de Windows Defender  
- Firewall de Windows Defender  
- SmartScreen de Windows Defender  
- Cifrado de Windows  
- Windows Defender Exploit Guard  
- Control de aplicaciones de Windows Defender  
- Centro de seguridad avanzada de Windows Defender  
- Protección contra amenazas avanzada de Windows Defender  
- Windows Information Protection  

Para más información sobre la característica de Intune, consulte [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configuración del dispositivo
<!--1357903-->

A partir de Configuration Manager 1806, la carga de trabajo de configuración de dispositivos incluye la configuración que administra para los dispositivos de la organización. Al cambiar esta carga de trabajo también se mueven las cargas de trabajo **Acceso a los recursos** y **Endpoint Protection**.

Todavía puede implementar la configuración de Configuration Manager en los dispositivos administrados conjuntamente, aunque Intune sea la autoridad de configuración de dispositivos. Esta excepción se podría usar para definir la configuración que necesita la organización, pero que todavía no está disponible en Intune. Especifique esta excepción en una [línea de base de configuración de Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Habilite la opción **Aplicar siempre esta línea de base, incluso para clientes administrados conjuntamente** al crear la línea de base. Puede cambiarla más adelante en la pestaña **General** de las propiedades de una línea de base existente.  

Para más información sobre la característica de Intune, consulte [Creación de un perfil de dispositivo en Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>Aplicaciones hacer clic y ejecutar de Office
<!--1357841-->

A partir de Configuration Manager 1806, esta carga de trabajo administra aplicaciones de Office 365 en dispositivos administrados en conjunto. 

- Después de mover la carga de trabajo, la aplicación se muestra en el **Portal de empresa** en el dispositivo.  

- Las actualizaciones de Office pueden tardar aproximadamente 24 horas en aparecer en el cliente a menos que se reinicien los dispositivos.  

- Hay una nueva condición global, **¿Las aplicaciones de Office 365 están administradas por Intune en este dispositivo?** Esta condición se agrega de forma predeterminada como requisito a las nuevas aplicaciones de Office 365. Cuando se realiza la transición de esta carga de trabajo, los clientes con administración conjunta no cumplen el requisito en la aplicación. Por tanto, no instalan Office 365 implementado a través de Configuration Manager.  

Para más información sobre la característica de Intune, consulte [Asignación de aplicaciones de Office 365 a dispositivos Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>Aplicaciones cliente
<!--1357892-->

A partir de Configuration Manager 1806, use Intune para administrar las aplicaciones cliente en dispositivos Windows 10 administrados en conjunto. Después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software.

Para más información sobre la característica de Intune, consulte [¿Qué es la administración de aplicaciones de Microsoft Intune?](https://docs.microsoft.com/intune/app-management) 

> [!Note]  
> La carga de trabajo de aplicaciones cliente es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Pasos siguientes

[How to switch workloads](/sccm/comanage/how-to-switch-workloads) (Cambio de las cargas de trabajo)  


