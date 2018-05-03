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
ms.openlocfilehash: 1657cbacde468ef7c54f95524e0fa9607a1a0186
ms.sourcegitcommit: e23350fe65ff99228274e465b24b5e163769f38f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/20/2018
---
# <a name="co-management-for-windows-10-devices"></a>Administración conjunta para dispositivos de Windows 10    
 Con actualizaciones anteriores de Windows 10 ya puede unir un dispositivo Windows 10 a Active Directory (AD) local y Azure AD en la nube al mismo tiempo (Azure AD híbrido). A partir de la Configuration Manager versión 1710, la administración conjunta aprovecha esta mejora y permite administrar dispositivos Windows 10 versión 1709 de forma simultánea mediante Configuration Manager e Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>¿Por qué administración conjunta?
Muchos clientes quieren administrar dispositivos de Windows 10 de la misma manera que administran dispositivos móviles mediante una solución simplificada, basada en la nube y de costo inferior, pero llevar a cabo la transición de la administración tradicional a una administración moderna puede resultar complicado.  
## <a name="what-is-co-management"></a>¿Qué es administración conjunta?
La administración conjunta le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager e Intune. Se trata de una solución que sirve de puente entre la administración tradicional y moderna, y proporciona un camino para realizar la transición con un enfoque por fases.

## <a name="benefits"></a>Ventajas 
- Uso inmediato de las características de Intune 
    - Acciones remotas
        - [Restablecimiento de la configuración de fábrica](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
        - [Borrado selectivo](https://docs.microsoft.com/intune/apps-selective-wipe)
        - [Eliminar dispositivos](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
        - [Reiniciar dispositivo](https://docs.microsoft.com/intune/device-restart)
        - [Empezar de cero](https://docs.microsoft.com/intune/device-fresh-start)
    - Orquestación con Intune para las cargas de trabajo siguientes:
        - [Directivas de cumplimiento](https://docs.microsoft.com/intune/device-compliance-get-started)
        - [Directivas de acceso a recursos](https://docs.microsoft.com/intune/device-profiles)
        - [Directivas de Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
        - [Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10), a partir de Configuration Manager 1802. <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Configuración de la administración conjunta
Hay dos formas de conseguir la administración conjunta. Una es que los dispositivos Windows 10 administrados mediante Configuration Manager y los dispositivos unidos a Azure AD híbrido se inscriban en Intune. La otra es que los dispositivos aprovisionados por Intune que se inscriben en Intune y, luego, se instalan con cliente de Configuration Manager obtengan un estado de administración conjunta.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Actualización a Configuration Manager versión 1710 o posterior.


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [Unidos a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (unidos a AD y a Azure AD).
  - [Habilitación de la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Configuración de la suscripción a Intune.](/sccm/mdm/deploy-use/configure-intune-subscription) o https://docs.microsoft.com/en-us/intune/setup-steps
 - [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)


### <a name="enable-co-management"></a>Habilitación de la administración conjunta 
 En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta). Seleccione  **Configure co-management** (Configurar administración conjunta) en la cinta para abrir el **Co-management Onboarding Wizard** (Asistente para incorporación de la administración conjunta). 
   
1. En la página **Suscripción**, haga clic en **Iniciar sesión** e inicie sesión en el inquilino de Intune y luego haga clic en **Siguiente**.    
2. En la página **Habilitación**, elija la opción **Automatic enrollment into Intune** (Inscripción automática en Intune). Copie la línea de comandos para los dispositivos ya inscritos en Intune, si es necesario. 
3. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune.
4. En la página **Almacenamiento provisional**, seleccione una colección de dispositivos para que sea la **Recopilación piloto**. Revise el **Resumen** y finalice el asistente. 

### <a name="upgrade-windows-10-client"></a>Actualización del cliente de Windows 10
- Actualización a [Windows 10, versión 1709 (también denominada "Fall Creators Update") y posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)

### <a name="configure-workloads-to-switch-to-intune"></a>Configuración de cargas de trabajo para cambiar a Intune 
El artículo [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) muestra cómo cambiar determinadas cargas de trabajo de Configuration Manager a Intune. El artículo también incluye instrucciones sobre cómo cambiar los grupos de dispositivos para los que se realiza la transición de las cargas de trabajo.

- **Directivas de cumplimiento:** definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. Para obtener más información, vea [Directivas de cumplimiento de dispositivos](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Directivas de Windows Update:** las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Para obtener más información, vea [Configuración de directivas de aplazamiento de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Directivas de acceso a recursos:** configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos. Para obtener más información, consulte el artículo sobre cómo [implementar perfiles de acceso a recursos](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** a partir de Configuration Manager 1802, la carga de trabajo de Endpoint Protection se puede pasar a Intune. Para obtener más información, vea [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10) <!-- 1357365 --> y [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune)


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalación del cliente Configuration Manager en los dispositivos inscritos en Intune
Al inscribir dispositivos de Windows 10 en Intune, puede instalar en ellos el cliente de Configuration Manager ([con un argumento de línea de comandos específico](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) para preparar los clientes para la administración conjunta. Luego podrá habilitar la administración conjunta desde la consola de Configuration Manager para empezar a trasladar cargas de trabajo específicas a Intune para dispositivos específicos de Windows 10.
Para los dispositivos de Windows 10 que todavía no están inscritos en Intune, puede usar la inscripción automática en Azure para inscribirlos. Para los nuevos dispositivos Windows 10, puede usar [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para definir la configuración rápida (OOBE), que incluye la inscripción automática, que inscribe dispositivos en Intune.
 - Habilitación de [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) en Configuration Manager (solo cuando se use Intune para instalar el cliente de Configuration Manager).

## <a name="monitor-co-management"></a>Supervisión de la administración conjunta
[El panel de administración conjunta](/sccm/core/clients/manage/co-management-dashboard) le ayudará a revisar las máquinas que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.


## <a name="next-steps"></a>Pasos siguientes
[Preparación de dispositivos Windows 10 para la administración conjunta](co-management-prepare.md)
