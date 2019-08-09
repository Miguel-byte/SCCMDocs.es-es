---
title: Administración de Windows Device Guard
titleSuffix: Configuration Manager
description: Aprenda a usar Configuration Manager para administrar Windows Device Guard.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 82f262b01129452da7c34ffb6f1a1bb2f15be8a8
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2019
ms.locfileid: "68533813"
---
# <a name="device-guard-management-with-configuration-manager"></a>Administración de Device Guard con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

## <a name="introduction"></a>Introducción
Device Guard es un grupo de características de Windows 10 que se han diseñado para proteger a los equipos frente a malware y otro software que no es de confianza. Evita la ejecución de código malintencionado al garantizar que solo se pueda ejecutar código aprobado que conoce.

Device Guard incluye una funcionalidad de seguridad basada en software y hardware. Control de aplicaciones de Windows Defender es una capa de seguridad basada en software que exige una lista explícita de software que se puede ejecutar en un equipo. Por sí solo, el control de aplicaciones no tiene ningún requisito previo de hardware ni firmware. Las directivas de control de aplicaciones que se implementan con Configuration Manager habilitan una directiva en equipos de colecciones de destino que cumplen con los requisitos de SKU y de versión mínima de Windows que se describen en este artículo. Si quiere, la protección basada en hipervisor de directivas de control de aplicaciones implementadas con Configuration Manager se puede habilitar mediante una directiva de grupo en hardware compatible.

Para obtener más información sobre Device Guard, consulte la [guía de implementación de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

   > [!NOTE]
   > A partir de Windows 10, versión 1709, las directivas de integridad de código configurables se denominan control de aplicaciones de Windows Defender.

## <a name="using-device-guard-with-configuration-manager"></a>Uso de Device Guard con Configuration Manager

Puede usar Configuration Manager para implementar una directiva de control de aplicaciones de Windows Defender. Esta directiva permite configurar el modo en el que Device Guard se ejecuta en equipos de una colección. 

Configure uno de los siguientes modos:

1. **Cumplimiento habilitado**: solo se pueden ejecutar archivos ejecutables de confianza.
2. **Solo auditoría**: permite la ejecución de todos los archivos ejecutables, pero registra los archivos ejecutables que se ejecutan en el registro de eventos del cliente local.

> [!Tip]  
> Esta característica se introdujo por primera vez en la versión 1702 como una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1906, ya no es de versión preliminar.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>¿Qué se puede ejecutar cuando se implementa una directiva de Windows Defender Application Control?

Windows Device Guard le permite controlar ampliamente lo que se puede ejecutar en los equipos que administra. Esta característica puede resultar útil para los equipos de los departamentos de alta seguridad, en los que es esencial que el software no deseado no se pueda ejecutar.

Al implementar una directiva, por lo general, se pueden ejecutar los siguientes archivos ejecutables:

- Componentes del sistema operativo Windows
- Controladores del Centro de desarrollo de hardware (con firmas de Laboratorios de calidad de hardware de Windows [WHQL])
- Aplicaciones de la Tienda Windows
- Cliente de Configuration Manager 
- Todo el software implementado mediante Configuration Manager que los equipos instalan después de procesar la directiva de Windows Defender Application Control. 
- Actualizaciones de componentes de Windows de:
    - Windows Update
    - Windows Update para empresas
    - Windows Server Update Services
    - Configuration Manager
    - También puede ejecutar software de confianza con una buena reputación, según determine Microsoft Intelligent Security Graph (ISG). ISG está formado por Windows Defender SmartScreen y otros servicios de Microsoft. Para que el software sea de confianza, el dispositivo debe ejecutar Windows Defender SmartScreen y Windows 10 versión 1709.

>[!IMPORTANT]
>Estos elementos no incluyen software que *no* esté integrado en Windows y que se actualice automáticamente desde actualizaciones de software de terceros o de Internet, tanto si se instalan a través de cualquiera de los mecanismos de actualización mencionados anteriormente como desde Internet. Solo se pueden ejecutar los cambios en el software que se implementen a través del cliente de Configuration Manager.

## <a name="before-you-start"></a>Antes de empezar

Antes de configurar o implementar directivas de Windows Defender Application Control, lea la siguiente información:

- La administración de Device Guard es una característica de versión preliminar de Configuration Manager y está sujeta a cambios.
- Para utilizar Device Guard con Configuration Manager, los equipos que administra deben ejecutar Windows 10 Enterprise versión 1703, o posterior.
- Después de procesar correctamente una directiva en un equipo cliente, Configuration Manager se configura como instalador administrado en ese cliente. El software que se implementa a través de él, después de que se procese la directiva, pasa a ser automáticamente de confianza. El software que instala Configuration Manager antes de que se procese la directiva de control de aplicaciones de Windows Defender no pasa a ser de confianza automáticamente.
- Los equipos cliente deben tener conectividad con el controlador de dominio a fin de poder procesar una directiva de Windows Defender Application Control correctamente.
- La programación de evaluación de cumplimiento predeterminada de las directivas de Control de aplicaciones, que se puede configurar durante la implementación, se realiza cada día. Si se observan problemas de procesamiento de la directiva, puede resultar útil configurar la programación de evaluación de cumplimiento para que sea más corta, por ejemplo, cada hora. Esta programación determina la frecuencia con la que los clientes intentan volver a procesar una directiva de control de aplicaciones de Windows Defender en caso de error.
- Independientemente del modo de cumplimiento que seleccione, al implementar una directiva de Windows Defender Application Control, los equipos cliente no pueden ejecutar aplicaciones de HTML con la extensión .hta.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Creación de directivas de Windows Defender Application Control
1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Control de aplicaciones de Windows Defender**.
3. En el grupo **Crear** de la pestaña **Inicio**, haga clic en **Crear directiva de control de aplicaciones**.
4. En la página **General** del **Asistente para crear directivas de Control de aplicaciones**, especifique la configuración siguiente:
    - **Nombre**: escriba un nombre único para esta directiva de Windows Defender Application Control. 
    - **Descripción**: si quiere, escriba una descripción de la directiva que lo ayude a identificarla en la consola de Configuration Manager.
    - **Fuerce un reinicio de dispositivos para que esta directiva se pueda aplicar a todos los procesos**: después de procesar la directiva en un equipo cliente, se programa un reinicio en el cliente según la opción **Configuración de cliente** para **Reinicio de equipo**.
        - Los dispositivos con Windows 10, versión 1703 o anteriores, se reinician siempre automáticamente.
        - A partir de Windows 10 versión 1709, a las aplicaciones que se ejecutan actualmente en el dispositivo no se les aplicará la nueva directiva de Control de aplicaciones hasta después del reinicio. Pero, las aplicaciones iniciadas después que se aplique la directiva cumplirán la nueva directiva de Control de aplicaciones. 
    - **Modo de cumplimiento**: elija uno de los siguientes métodos de cumplimiento de Device Guard en el equipo cliente.
        - **Cumplimiento habilitado**: solo se permiten archivos ejecutables de confianza.
        - **Solo auditoría**: permite la ejecución de todos los archivos ejecutables, pero registra los archivos ejecutables que se ejecutan en el registro de eventos del cliente local.
5. En la pestaña **Inclusiones** del **Asistente para crear directivas de Control de aplicaciones**, puede elegir **Autorizar el software de confianza para Intelligent Security Graph**.
6. Haga clic en **Agregar** si quiere agregar la relación de confianza a determinados archivos o carpetas en los equipos. En el cuadro de diálogo **Agregar archivo o carpeta de confianza**, puede especificar un archivo local o una ruta de acceso de carpeta de confianza. También puede especificar una ruta de acceso de archivo o carpeta en un dispositivo remoto en el que tenga permiso para conectarse. Cuando agregue confianza para determinados archivos y carpetas en una directiva de control de aplicaciones de Windows Defender, puede realizar lo siguiente:
    - Solucionar problemas con los comportamientos de instalador administrado
    - Confiar en aplicaciones de línea de negocio que no se pueden implementar con Configuration Manager
    - Confiar en aplicaciones que se incluyen en una imagen de implementación de sistema operativo 
8. Haga clic en **Siguiente** para completar el asistente.

>[!IMPORTANT]
>La inclusión de carpetas o archivos de confianza solo se admite en los equipos cliente que ejecutan la versión 1706 o posterior del cliente de Configuration Manager. Si las reglas de inclusión están englobadas en una directiva de Windows Defender Application Control y esta última se implementa en un equipo cliente que ejecuta una versión anterior del cliente de Configuration Manager, no podrá aplicarse. Actualizar estos clientes anteriores resolverá este problema. Todavía se pueden aplicar directivas que no engloban ninguna regla de inclusión en las versiones anteriores del cliente de Configuration Manager.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Implementación de directivas de Windows Defender Application Control
1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Control de aplicaciones de Windows Defender**.
3. En la lista de directivas, seleccione la que quiera implementar y luego, en el grupo **Implementación** de la pestaña **Inicio**, haga clic en **Implementar la directiva de control de aplicaciones**.
4. En el cuadro de diálogo **Implementar la directiva de control de aplicaciones**, seleccione la colección en la que quiere implementar la directiva. A continuación, configure una programación para determinar cuándo los clientes evalúan la directiva. Por último, seleccione si el cliente puede evaluar la directiva fuera de las ventanas de mantenimiento configuradas.
5. Cuando haya terminado, haga clic en **Aceptar** para implementar la directiva. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Supervisión de directivas de Windows Defender Application Control

Utilice la información del artículo [Supervisión de la configuración de cumplimiento](/sccm/compliance/deploy-use/monitor-compliance-settings) a fin de poder supervisar que la directiva implementada se ha aplicado correctamente a todos los equipos.

Para supervisar el procesamiento de una directiva de Windows Defender Application Control, utilice el siguiente archivo de registro en los equipos cliente:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para comprobar el software específico que se bloquea o audita, vea los siguientes registros de eventos de cliente local:

1. Para bloquear y auditar archivos ejecutables, utilice **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **Integridad de código** > **Operativo**.
2. Para bloquear y auditar Windows Installer y archivos de script, utilice **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **AppLocker** > **MSI y script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-device-guard"></a>Información de seguridad y privacidad para Device Guard

- En esta versión preliminar, no implemente directivas de Windows Defender Application Control con el modo de cumplimiento **Solo auditoría** en un entorno de producción. Este modo está diseñado para ayudarle a probar la funcionalidad solo en una configuración de laboratorio.
- Los dispositivos que tienen una directiva implementada en el modo **Solo auditoría** o **Cumplimiento habilitado** que no se hayan reiniciado para aplicar la directiva, son vulnerables al software que se instale que no sea de confianza.
En esta situación, el software podría seguir teniendo permiso para ejecutarse incluso si se reinicia el dispositivo, o recibe una directiva en modo **Cumplimiento habilitado**.
- Para asegurarse de que la directiva de Windows Defender Application Control es eficaz, prepare el dispositivo en un entorno de laboratorio. A continuación, implemente la directiva **Cumplimiento habilitado** y, por último, reinicie el dispositivo antes de enviar el dispositivo a un usuario final.
- No implemente una directiva con **Cumplimiento habilitado** y, a continuación, una directiva con **Solo auditoría** en el mismo dispositivo. Esta configuración puede provocar la ejecución de software que no es de confianza.
- Cuando se usa Configuration Manager para habilitar Control de aplicaciones de Windows Defender en los equipos cliente, la directiva no evita que los usuarios con derechos de administrador local sorteen las directivas de Control de aplicaciones o ejecuten de otro modo software que no es de confianza. 
- La única manera de evitar que los usuarios con derechos de administrador local deshabiliten el Control de aplicaciones consiste en implementar una directiva binaria firmada. Esta implementación es posible a través de la directiva de grupo, pero no se admite actualmente en Configuration Manager.
- La configuración de Configuration Manager como un instalador administrado en los equipos cliente utiliza la directiva de AppLocker. AppLocker solo se usa para identificar los instaladores administrados y todo el cumplimiento tiene lugar con Control de aplicaciones de Windows Defender. 




