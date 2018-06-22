---
title: Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar perfiles de Wi-Fi, VPN, correo electrónico y certificado en System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: faf8d48614bc3e27381d57d86fc24da9356aa3f0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347576"
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Implementar perfiles de VPN en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para poder usar perfiles, deben estar implementados en una o varias recopilaciones.  

 Use el cuadro de diálogo **Implementar perfil de Wi-Fi**, **Implementar perfil de VPN**, **Implementar el perfil de Exchange ActiveSync** o **Deploy Certificate Profile** (Implementar perfil de certificado) para configurar la implementación de estos perfiles. Como parte de la configuración, defina la recopilación en la que se implementará el perfil y especifique la frecuencia con la que se evaluará la compatibilidad del perfil.  

> [!NOTE]  
>  Si implementa varios perfiles de acceso a recursos de empresa en el mismo usuario, ocurre lo siguiente:  
>   
>  -   Si una configuración en conflicto contiene un valor opcional, no se enviará al dispositivo.  
> -   Si una configuración en conflicto contiene un valor obligatorio, se enviará al dispositivo el valor predeterminado. Si no hay ningún valor predeterminado, se producirá un error en el perfil de acceso de recursos de toda la empresa. Por ejemplo, si implementa dos perfiles de correo electrónico en el mismo usuario y los valores especificados para **Host de Exchange ActiveSync** o **Dirección de correo electrónico** son diferentes, se producirá un error en ambos perfiles de correo electrónico ya que son parámetros obligatorios.  

> -   Para implementar perfiles de certificado, primero debe configurar la infraestructura y crear perfiles de certificado. Para obtener más información, consulte los temas siguientes:  
>   
>  -   [Configuring certificate infrastructure in System Center Configuration Manager](certificate-infrastructure.md) (Configuración de infraestructura de certificados en System Center Configuration Manager)  
> -   [How to create certificate profiles in System Center Configuration Manager](create-certificate-profiles.md) (Cómo crear perfiles de certificado en System Center Configuration Manager)    

> [!IMPORTANT]  
>  Si se quita una implementación de perfil de VPN, este no se quita de los dispositivos cliente. Si desea quitar el perfil de los dispositivos, deberá hacerlo manualmente
>   

## <a name="deploying--profiles"></a>Implementar perfiles  


1.  En la consola de System Center Configuration Manager, elija **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía** y elija el tipo de perfil adecuado, como **Perfiles de Wi-Fi**.  

3.  En la lista de perfiles, seleccione el perfil que quiera implementar y, después, en la pestaña **Inicio**, en el grupo **Implementación**, haga clic en **Implementar**.  

4.  En el cuadro de diálogo para implementar el perfil, especifique la información siguiente:  

    -   **Recopilación**: haga clic en **Examinar** para seleccionar la recopilación en la que quiere implementar el perfil.  

    -   **Generar una alerta**: habilite esta opción para configurar una alerta que se genera si la compatibilidad del perfil es inferior a un determinado porcentaje en una hora y fecha especificadas. También puede especificar si desea que se envíe una alerta a System Center Operations Manager.  

    -   -   **Retraso aleatorio (horas)**: (solo para perfiles de certificado que contienen la configuración del Protocolo de inscripción de certificados simple). Especifica una ventana de retraso para evitar un procesamiento excesivo en el Servicio de inscripción de dispositivos de red. El valor predeterminado es **64** horas.  

    -   **Especifique la programación de evaluación de compatibilidad para este perfil de <type>**: especifique la programación de evaluación del perfil implementado en equipos cliente. La programación puede ser simple o personalizada.  

        > [!NOTE]  
        >  Los equipos cliente evalúan el perfil cuando el usuario inicia sesión.  

5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo y crear la implementación.

### <a name="see-also"></a>Consulte también  

[How to monitor Wi-Fi, VPN, and email profiles in System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md) (Cómo supervisar perfiles de Wi-Fi, VPN y correo electrónico en System Center Configuration Manager)

[How to monitor certificate profiles in System Center Configuration Manager](monitor-certificate-profiles.md) (Cómo supervisar perfiles de certificado en System Center Configuration Manager)
