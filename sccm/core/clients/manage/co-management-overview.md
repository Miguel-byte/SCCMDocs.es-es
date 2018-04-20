---
title: Administración conjunta para dispositivos de Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: a5ceea5502e4eb2785946e1dd3bc9ed0842daf25
ms.sourcegitcommit: d8a4a53630351b3d677bbdc5d203e7d330472cba
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="co-management-for-windows-10-devices"></a>Administración conjunta para dispositivos de Windows 10    
<!-- 1350871 -->
Muchos clientes quieren administrar dispositivos de Windows 10 de la misma manera que administran dispositivos móviles mediante una solución simplificada, basada en la nube y de costo inferior, pero llevar a cabo la transición de la administración tradicional a una administración moderna puede resultar complicado. Las actualizaciones anteriores de Windows 10 ya permiten unir un dispositivo Windows 10 a Active Directory (AD) local y en la nube al mismo tiempo (Azure AD híbrido). A partir de la versión 1710 de Configuration Manager, la administración conjunta aprovecha esta mejora y permite administrar dispositivos de la versión 1709 de Windows 10 (también conocida con el nombre Fall Creators Update) de forma simultánea mediante Intune y Configuration Manager. Se trata de una solución que sirve de puente entre la administración tradicional y moderna, y proporciona un camino para realizar la transición con un enfoque por fases. 

Hay dos formas de conseguir la administración conjunta.  Una es que los dispositivos Windows 10 administrados mediante Configuration Manager y los dispositivos unidos a Azure AD híbrido se inscriban en Intune. La otra es que los dispositivos aprovisionados por Intune que se inscriben en Intune y, luego, se instalan con cliente de Configuration Manager obtengan un estado de administración conjunta.

## <a name="prerequisites"></a>Requisitos previos
Debe cumplir los siguientes requisitos previos para poder habilitar la administración conjunta. Hay requisitos previos generales y distintos requisitos previos para los clientes con el cliente de Configuration Manager y los dispositivos que no tienen instalado el cliente.

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.

### <a name="general-prerequisites"></a>Requisitos previos generales
A continuación se indican los requisitos previos generales para poder habilitar la administración conjunta:  

- Versión 1710 de Configuration Manager o posterior
- Azure AD
- Licencia de EMS o de Intune para todos los usuarios
- [Inscripción automática con Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitada
- Suscripción a Intune &#40;entidad de MDM en Intune establecida en **Intune**&#41;


   > [!Note]  
   > Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos con el cliente de Configuration Manager
- Windows 10, versión 1709 (también conocida como "Fall Creators Update") y posterior
- [Unidos a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (unidos a AD y a Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos sin el cliente de Configuration Manager
- Windows 10, versión 1709 (también conocida como "Fall Creators Update") y posterior
- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) en Configuration Manager (al usar Intune para instalar el cliente de Configuration Manager)

## <a name="workloads-you-can-switch-to-intune"></a>Cargas de trabajo que puede pasar a Intune
Después de habilitar la administración conjunta, Configuration Manager sigue administrando todas las cargas de trabajo. Cuando decida que ya está listo, puede hacer que Intune empiece a administrar las cargas de trabajo disponibles. Puede hacer que Intune administre las siguientes cargas de trabajo:   

### <a name="compliance-policies"></a>Directivas de cumplimiento
Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. Para obtener más información, vea [Directivas de cumplimiento de dispositivos](/sccm/mdm/deploy-use/device-compliance-policies).  

### <a name="windows-update-for-business-policies"></a>Directivas de Windows Update para empresas
Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Para obtener más información, vea [Configuración de directivas de aplazamiento de Windows Update para empresas](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="resource-access-policies"></a>Directivas de acceso a recursos
Las directivas de acceso a recursos configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos. Para obtener más información, consulte el artículo sobre cómo [implementar perfiles de acceso a recursos](/sccm/protect/deploy-use/deploy-wifi-vpn-email-cert-profiles).

### <a name="endpoint-protection"></a>Endpoint Protection 
<!-- 1357365 -->
A partir de Configuration Manager 1802, La carga de trabajo de Endpoint Protection se puede pasar a Intune. Para obtener más información, vea [Cambiar las cargas de trabajo a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) y [Endpoint Protection en Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

## <a name="architectural-overview-for-co-management"></a>Introducción a la arquitectura de la administración conjunta
En el siguiente diagrama se muestra una introducción a la arquitectura de la administración conjunta y cómo encaja en las infraestructuras existentes de Intune y de Configuration Manager.

![Diagrama de arquitectura de administración conjunta](./media/co-management-arch.svg)

## <a name="scenarios-to-enable-co-management"></a>Escenarios para habilitar la administración conjunta  
Puede habilitar la administración conjunta para los dispositivos de Windows 10 inscritos en Microsoft Intune y para los clientes existentes de Configuration Manager que tienen Windows 10. En ambos escenarios, los dispositivos de Windows 10 se administran de forma simultánea con Intune y Configuration Manager, y se unen a AD y a Azure AD.  

### <a name="devices-enrolled-in-intune"></a>Dispositivos inscritos en Intune  
Al inscribir dispositivos de Windows 10 en Intune, puede instalar en ellos el cliente de Configuration Manager (con un argumento de línea de comandos específico) para preparar los clientes para la administración conjunta. Luego podrá habilitar la administración conjunta desde la consola de Configuration Manager para empezar a trasladar cargas de trabajo específicas a Intune para dispositivos específicos de Windows 10.  

Para los dispositivos de Windows 10 que todavía no están inscritos en Intune, puede usar la inscripción automática en Azure para inscribirlos. Para los nuevos dispositivos Windows 10, puede usar [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para definir la configuración rápida (OOBE), que incluye la inscripción automática, que inscribe dispositivos en Intune.  

### <a name="configuration-manager-clients"></a>Clientes de Configuration Manager
Si tiene dispositivos de Windows 10 que son clientes de Configuration Manager, puede inscribirlos y habilitar la administración conjunta desde la consola de Configuration Manager. Configuration Manager desencadena la inscripción automática en Intune en función de la información del inquilino de Azure AD.  


## <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Acciones remotas disponibles en Intune para Azure para los dispositivos administrados conjuntamente
Si un dispositivo de Windows 10 está habilitado para la administración conjunta, tiene a su disposición las siguientes acciones remotas de Intune en Azure:  
- [Restablecimiento de la configuración de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Borrado selectivo](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
- [Empezar de cero](https://docs.microsoft.com/intune/device-fresh-start)

## <a name="next-steps"></a>Pasos siguientes
[Preparación de dispositivos Windows 10 para la administración conjunta](co-management-prepare.md)
