---
title: Cargas de trabajo de administración conjunta
titleSuffix: Configuration Manager
description: Obtenga información sobre las cargas de trabajo que se puede cambiar de Configuration Manager a Microsoft Intune.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755553"
---
# <a name="co-management-workloads"></a>Cargas de trabajo de administración conjunta

No tiene que cambiar las cargas de trabajo, o puede realizarlas por separado cuando esté listo. Configuration Manager sigue administrando todas las otras cargas de trabajo, incluidas las cargas de trabajo que no cambie a Intune y no es compatible con todas las demás características de Configuration Manager que la administración conjunta.

Administración conjunta es compatible con las cargas de trabajo siguientes:

- [Directivas de cumplimiento](#compliance-policies)  

- [Directivas de Windows Update](#windows-update-policies)  

- [Directivas de acceso a recursos](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuración del dispositivo](#device-configuration)  

- [Hacer clic para ejecutar aplicaciones de Office](#office-click-to-run-apps)  

- [Aplicaciones cliente](#client-apps)  



## <a name="compliance-policies"></a>Directivas de cumplimiento 

Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. 

Para obtener más información sobre la característica de Intune, consulte [las directivas de cumplimiento de dispositivo](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Directivas de Windows Update

Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. 

Para obtener más información sobre la característica de Intune, consulte [configuración de directivas de aplazamiento Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Directivas de acceso a recursos

Las directivas de acceso a recursos configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos. 

Para obtener más información sobre la característica de Intune, consulte [implementar perfiles de acceso a recursos](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

A partir de Configuration Manager 1802, la carga de trabajo de Endpoint Protection incluye el conjunto de Windows Defender de características de protección antimalware: 

- Protección de aplicaciones de Windows Defender  
- Firewall de Windows Defender  
- SmartScreen de Windows Defender  
- Cifrado de Windows  
- Windows Defender Exploit Guard  
- Control de aplicaciones de Windows Defender  
- Centro de seguridad avanzada de Windows Defender  
- Protección contra amenazas avanzada de Windows Defender  
- Windows Information Protection  

Para obtener más información sobre la característica de Intune, consulte [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configuración del dispositivo
<!--1357903-->

A partir de Configuration Manager 1806, la carga de trabajo de configuración del dispositivo incluye opciones que administrar para los dispositivos de su organización. El cambio de esta carga de trabajo también mueve la **acceso a los recursos** y **Endpoint Protection** cargas de trabajo.

Todavía puede implementar la configuración de Configuration Manager en los dispositivos administrados conjuntamente, aunque Intune sea la autoridad de configuración de dispositivos. Esta excepción podría utilizarse para configurar las opciones que su organización necesita, pero aún no están disponible en Intune. Especifique esta excepción en una [línea de base de configuración de Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Habilitar la opción de **siempre se aplican a esta línea base incluso para los clientes administrados conjuntamente** al crear la línea base. Puede cambiarla más adelante el **General** ficha de las propiedades de una instantánea existente.  

Para obtener más información sobre la característica de Intune, consulte [crear un perfil de dispositivo en Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>Aplicaciones hacer clic y ejecutar de Office
<!--1357841-->

A partir de Configuration Manager 1806, esta carga de trabajo administra las aplicaciones de Office 365 en dispositivos administrados conjuntamente. 

- Después de mover la carga de trabajo, la aplicación se muestra en el **Portal de empresa** en el dispositivo.  

- Las actualizaciones de Office pueden tardar aproximadamente 24 horas en aparecer en el cliente a menos que se reinicien los dispositivos.  

- Hay una nueva condición global, **¿Las aplicaciones de Office 365 están administradas por Intune en este dispositivo?** Esta condición se agrega de forma predeterminada como requisito a las nuevas aplicaciones de Office 365. Cuando se realiza la transición de esta carga de trabajo, los clientes con administración conjunta no cumplen el requisito en la aplicación. Por tanto, no instalan Office 365 implementado a través de Configuration Manager.  

Para obtener más información sobre la característica de Intune, consulte [aplicaciones asignar Office 365 a dispositivos Windows 10 con Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>Aplicaciones cliente
<!--1357892-->

A partir de Configuration Manager versión 1806, usar Intune para administrar las aplicaciones cliente en dispositivos Windows 10 administrados conjuntamente. Después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software.

Para obtener más información sobre la característica de Intune, consulte [¿qué es la administración de aplicaciones de Microsoft Intune?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> La carga de trabajo de aplicaciones de cliente es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Pasos siguientes

[Cómo cambiar las cargas de trabajo](/sccm/comanage/how-to-switch-workloads)  


