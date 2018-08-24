---
title: Administración conjunta para dispositivos de Windows 10
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager y Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: a99983583aa8c21f8a987f3e20550752e7b77ba4
ms.sourcegitcommit: 83806460b6fd88a1d08a2c97f4d72b9e36e04102
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39495567"
---
# <a name="co-management-for-windows-10-devices"></a>Administración conjunta para dispositivos de Windows 10    

Con actualizaciones anteriores de Windows 10 ya puede unir un dispositivo Windows 10 a Active Directory (AD) local y Azure AD en la nube al mismo tiempo (Azure AD híbrido). A partir de la versión 1710 Configuration Manager, la administración conjunta aprovecha esta mejora. Le permite administrar simultáneamente dispositivos Windows 10 versión 1709 mediante Configuration Manager e Intune. <!-- 1350871 -->


## <a name="why-co-management"></a>¿Por qué administración conjunta?

Muchos clientes quieren administrar dispositivos de Windows 10 de la misma manera que administran dispositivos móviles mediante una solución simplificada, basada en la nube y de costo inferior, pero llevar a cabo la transición de la administración tradicional a una administración moderna puede resultar complicado.  


## <a name="what-is-co-management"></a>¿Qué es administración conjunta?

La administración conjunta le permite administrar simultáneamente dispositivos Windows 10 mediante Configuration Manager e Intune. Se trata de una solución que sirve de puente entre la administración tradicional y moderna, y proporciona un camino para realizar la transición con un enfoque por fases.


## <a name="benefits"></a>Ventajas 

Uso inmediato de las siguientes características de Intune:  
 
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
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10), a partir de Configuration Manager 1802. <!-- 1357365 -->
    - [Configuración de dispositivo](https://docs.microsoft.com/intune/device-profile-create), a partir de la versión 1806 de Configuration Manager. <!-- 1357903 -->
    - [Aplicaciones hacer clic y ejecutar de Office](https://docs.microsoft.com/intune/apps-add-office365), a partir de la versión 1806 de Configuration Manager <!--1357841-->
    - [Aplicaciones móviles](https://docs.microsoft.com/intune/app-management), a partir de Configuration Manager versión 1806 como una característica de versión preliminar. <!--1357892-->



## <a name="how-to-configure-co-management"></a>Configuración de la administración conjunta

 Hay dos formas de conseguir la administración conjunta:  

   - Configuration Manager proporciona administración conjunta: inscriba en Intune los dispositivos Windows 10 unidos a Azure AD que ya son clientes de Configuration Manager.  

   - Aprovisionados por Intune: para los dispositivos que ya están inscritos en Intune, instale el cliente de Configuration Manager para llegar a un estado de administración conjunta. 


### <a name="configuration-manager"></a>Configuration Manager

 -  Actualización a Configuration Manager versión 1710 o posterior.


### <a name="azure-active-directory"></a>Azure Active Directory

 - Los dispositivos Windows 10 deben estar unidos a Azure AD. Pueden ser cualquiera de los siguientes tipos:  

     - [Azure híbrido unido a AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup), donde el dispositivo está unido a Azure AD y el dominio local  

     - Solo unido a Azure AD. (Este tipo se conoce a veces como "unido al dominio en la nube")<!--SCCMDocs issue 605-->

 - [Habilite la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="intune"></a>Intune

 - [Cómo configurar la suscripción a Intune](/sccm/mdm/deploy-use/configure-intune-subscription) o [Configurar Intune](/intune/setup-steps)  

 - [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Habilitación de la administración conjunta 

 > [!Important]  
 > A partir de la versión 1802, para habilitar la administración conjunta, la cuenta de usuario administrativa en Configuration Manager debe ser un **Administrador total** con **Todos** los ámbitos de seguridad. Para obtener más información, vea [Fundamentals of role-based administration (Aspectos básicos de la administración basada en roles)](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Configurar administración conjunta** en la cinta para abrir el **Asistente para incorporación de la administración conjunta**. 
   
1. En la página **Suscripción**, haga clic en **Sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

    > [!Tip]   
    > Asegúrese de que la cuenta utilizada para iniciar sesión en el inquilino tiene asignada una licencia de Intune. En caso contrario, se producirá el error "Usuario no reconocido".  

2. En la página **Habilitación**, elija la opción **Inscripción automática en Intune**. Copie la línea de comandos para los dispositivos ya inscritos en Intune, si es necesario.  

    > [!Note]  
    > A partir de la versión 1806, la inscripción automática no es inmediata para todos los clientes. Este comportamiento ayuda a escalar la inscripción mejor para entornos de gran tamaño. Configuration Manager aleatoriza la inscripción según el número de clientes. Por ejemplo, si el entorno tiene 100 000 clientes, cuando se habilita esta configuración, la inscripción tiene lugar durante varios días.<!--1358003-->  

3. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune.  

4. En la página **Almacenamiento provisional**, seleccione una colección de dispositivos para que sea la **Recopilación piloto**. Revise el **Resumen** y finalice el asistente.  


### <a name="upgrade-windows-10-client"></a>Actualización del cliente de Windows 10

- Actualización a [Windows 10, versión 1709 (también denominada "Fall Creators Update") y posterior](/sccm/osd/deploy-use/manage-windows-as-a-service)


### <a name="configure-workloads-to-switch-to-intune"></a>Configuración de cargas de trabajo para cambiar a Intune 

El artículo [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) muestra cómo cambiar determinadas cargas de trabajo de Configuration Manager a Intune. El artículo también incluye instrucciones sobre cómo cambiar los grupos de dispositivos para los que se realiza la transición de las cargas de trabajo.

#### <a name="compliance-policies"></a>Directivas de cumplimiento 
Las directivas de cumplimiento definen las reglas y los valores de configuración que un dispositivo debe cumplir para que se considere conforme a las directivas de acceso condicional. Las directivas de cumplimiento también se pueden usar para supervisar y corregir problemas de compatibilidad con dispositivos independientemente del acceso condicional. Para obtener más información, vea [Directivas de cumplimiento de dispositivos](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### <a name="windows-update-policies"></a>Directivas de Windows Update
Las directivas de Windows Update para empresas le permiten configurar directivas de aplazamiento para actualizaciones de características de Windows 10 o actualizaciones de calidad para dispositivos con Windows 10 administradas directamente por Windows Update para empresas. Para obtener más información, vea [Configuración de directivas de aplazamiento de Windows Update para empresas](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### <a name="resource-access-policies"></a>Directivas de acceso a recursos
Las directivas de acceso a recursos configuran los ajustes de VPN, Wi-Fi, correo electrónico y certificados en los dispositivos. Para obtener más información, consulte el artículo sobre cómo [implementar perfiles de acceso a recursos](https://docs.microsoft.com/intune/device-profiles).

#### <a name="endpoint-protection"></a>Endpoint Protection
A partir de Configuration Manager 1802, La carga de trabajo de Endpoint Protection se puede pasar a Intune. Para obtener más información, vea [Endpoint Protection para Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> y [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### <a name="device-configuration"></a>Configuración del dispositivo
A partir de Configuration Manager 1806, la configuración de dispositivo se puede pasar a Intune. Para obtener más información, vea [Creación de un perfil de dispositivo en Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) y [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Aplicaciones hacer clic y ejecutar de Office
A partir de Configuration Manager 1806, la carga de trabajo de Office 365 se puede pasar a Intune. Para obtener más información, vea [Cargas de trabajo que se pueden pasar a Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### <a name="mobile-apps"></a>Aplicaciones móviles
A partir de la versión 1806 de Configuration Manager, la carga de trabajo se puede pasar a Intune. Esta es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features). Después de realizar la transición de esta carga de trabajo, las aplicaciones disponibles implementadas desde Intune están disponibles en el Portal de empresa. Las aplicaciones implementadas desde Configuration Manager están disponibles en el Centro de software.<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Instalación del cliente Configuration Manager en los dispositivos inscritos en Intune

Al inscribir dispositivos de Windows 10 en Intune, instale en ellos el cliente de Configuration Manager ([con una línea de comandos específica](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) para preparar los clientes para la administración conjunta. Luego podrá habilitar la administración conjunta desde la consola de Configuration Manager para empezar a trasladar cargas de trabajo específicas a Intune para dispositivos específicos de Windows 10.
Para los dispositivos de Windows 10 que todavía no están inscritos en Intune, use la inscripción automática en Azure para inscribirlos. Para los nuevos dispositivos Windows 10, use [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) para definir la configuración rápida (OOBE), que incluye la inscripción automática, que inscribe dispositivos en Intune.

Cuando utilice Intune para instalar el cliente de Configuration Manager, habilite [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) en Configuration Manager.



## <a name="monitor-co-management"></a>Supervisión de la administración conjunta

[El panel de administración conjunta](/sccm/core/clients/manage/co-management-dashboard) le ayudará a revisar las máquinas que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.



## <a name="next-steps"></a>Pasos siguientes

[Preparación de dispositivos Windows 10 para la administración conjunta](co-management-prepare.md)
