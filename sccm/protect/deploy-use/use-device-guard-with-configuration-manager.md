---
title: "Cómo administrar Windows Device Guard | Documentos de Microsoft"
description: Aprenda a usar System Center Configuration Manager para administrar Windows Device Guard.
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: dudeso
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
caps.latest.revision: "13"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3921748d3c99c2a35b670f3ca121dc7ab92d43bc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="device-guard-management-with-configuration-manager"></a>Administración de Device Guard con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

## <a name="introduction"></a>Introducción
Device Guard es un grupo de características de Windows 10 que se han diseñado para proteger a los equipos frente a malware y otro software que no es de confianza. Evita la ejecución de código malintencionado al garantizar que solo se pueda ejecutar código aprobado que conoce.

Device Guard incluye una funcionalidad de seguridad basada en software y hardware. La integridad de código configurable es una capa de seguridad basada en software que exige una lista explícita de software que se puede ejecutar en un equipo. Por sí sola, la integridad de código configurable no tiene ningún requisito previo de hardware o firmware. Las directivas de Device Guard implementadas con Configuration Manager permiten una directiva de integridad de código configurable en equipos de colecciones de destino que cumplen con la versión mínima de Windows y los requisitos de SKU que se describen en este tema. Si quiere, la protección basada en hipervisor de las directivas de integridad de código implementadas a través de Configuration Manager se puede habilitar mediante una directiva de grupo en el hardware que lo permita.

Para obtener más información sobre Device Guard, consulte la [guía de implementación de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide).

## <a name="using-device-guard-with-configuration-manager"></a>Uso de Device Guard con Configuration Manager

Puede usar Configuration Manager para implementar una directiva de Device Guard que le permita configurar el modo en que se ejecuta Device Guard en los equipos de una colección. 

Configure uno de los siguientes modos:

1.  **Cumplimiento habilitado**: solo se pueden ejecutar archivos ejecutables de confianza.
2.  **Solo auditoría**: permite la ejecución de todos los archivos ejecutables, pero registra los archivos ejecutables que se ejecutan en el registro de eventos del cliente local.

>[!TIP]
>En esta versión de Configuration Manager, Device Guard es una característica de versión preliminar. Para habilitarla, vea [Características de versión preliminar en System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).

## <a name="what-can-run-when-you-deploy-a-device-guard-policy"></a>¿Qué se puede ejecutar cuando se implementa una directiva de Device Guard?

Windows Device Guard le permite controlar ampliamente lo que se puede ejecutar en los equipos que administra. Esta característica puede resultar útil para los equipos de los departamentos de alta seguridad, en los que es esencial que el software no deseado no se pueda ejecutar.

Al implementar una directiva, por lo general, se pueden ejecutar los siguientes archivos ejecutables:

- Componentes del sistema operativo Windows
- Controladores del Centro de desarrollo de hardware (con firmas de Laboratorios de calidad de hardware de Windows [WHQL])
- Aplicaciones de la Tienda Windows
- Cliente de Configuration Manager 
- Todo el software implementado mediante Configuration Manager que los equipos instalan después de procesar la directiva de Device Guard. 
- Actualizaciones de componentes de Windows de:
    - Windows Update
    - Windows Update para empresas
    - Windows Server Update Services
    - Configuration Manager

>[!IMPORTANT]
>Estos elementos no incluyen software que *no* esté integrado en Windows y que se actualice automáticamente desde actualizaciones de software de terceros o de Internet, tanto si se instalan a través de cualquiera de los mecanismos de actualización mencionados anteriormente como desde Internet. Solo se pueden ejecutar los cambios en el software que se implementen a través del cliente de Configuration Manager.

## <a name="before-you-start"></a>Antes de empezar

Antes de configurar o implementar directivas de Device Guard, lea la siguiente información:

- La administración de Device Guard es una característica de versión preliminar de Configuration Manager y está sujeta a cambios.
- Para utilizar Device Guard con Configuration Manager, los equipos que administra deben ejecutar Windows 10 Enterprise versión 1703, o posterior.
- Una vez que se procesa una directiva correctamente en un equipo cliente, Configuration Manager se configura como un instalador administrado en ese cliente, y el software implementado a través de SCCM después de los procesos de directiva pasa a ser de confianza automáticamente. El software que instala Configuration Manager antes de los procesos de directivas de Device Guard no pasa a ser de confianza automáticamente.
- Los equipos cliente deben tener conectividad con el controlador de dominio a fin de poder procesar una directiva de Device Guard correctamente.
- La programación de evaluación de cumplimiento predeterminada para las directivas de Device Guard, que se puede configurar durante la implementación, se realiza cada día. Si se observan problemas de procesamiento de la directiva, puede resultar útil configurar la programación de evaluación de cumplimiento para que sea más corta, por ejemplo, cada hora. Esta programación determina con qué frecuencia los clientes intentan volver a procesar una directiva de Device Guard cuando se produce un error.
- Independientemente del modo de cumplimiento que seleccione, al implementar una directiva de Device Guard, los equipos cliente no pueden ejecutar aplicaciones de HTML con la extensión .hta.

## <a name="how-to-create-a-device-guard-policy"></a>Creación de una directiva de Device Guard
1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2.  En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Directivas de Device Guard**.
3.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear directiva de Device Guard**.
4.  En la página **General** de **Create Device Guard Policy Wizard** (Asistente para crear directivas de cumplimiento), especifique la configuración siguiente:
    - **Nombre**: escriba un nombre único para la directiva de Device Guard. 
    - **Descripción**: si quiere, escriba una descripción de la directiva que lo ayude a identificarla en la consola de Configuration Manager.
    - **Modo de cumplimiento**: elija uno de los siguientes métodos de cumplimiento de Device Guard en el equipo cliente.
        - **Cumplimiento habilitado**: solo se permiten archivos ejecutables de confianza.
        - **Solo auditoría**: permite la ejecución de todos los archivos ejecutables, pero registra los archivos ejecutables que se ejecutan en el registro de eventos del cliente local.
5.  En la pestaña **Inclusiones** de **Create Device Guard Policy Wizard** (Asistente para crear directivas de cumplimiento), haga clic en **Agregar** si desea agregar opcionalmente confianza para determinados archivos o carpetas en los equipos. 
6.  En el cuadro de diálogo **Agregar archivo o carpeta de confianza	**, especifique la información sobre el archivo o la carpeta en que desea confiar. Puede especificar una ruta de acceso de archivo o carpeta local o conectarse a un dispositivo remoto para el que tiene permiso para conectarse y especificar una ruta de acceso de archivo o carpeta en dicho dispositivo.
Cuando agregue confianza para determinados archivos y carpetas en una directiva de Device Guard, puede:
    - Solucionar problemas con los comportamientos de instalador administrado
    - Confiar en aplicaciones de línea de negocio que no se pueden implementar con Configuration Manager
    - Confiar en aplicaciones que se incluyen en una imagen de implementación de sistema operativo 
7.  Haga clic en **Siguiente** y complete el asistente.

>[!IMPORTANT]
>La inclusión de carpetas o archivos de confianza solo se admite en los equipos cliente que ejecutan la versión 1706 o posterior del cliente de Configuration Manager. Si las reglas de inclusión están englobadas en una directiva de Device Guard y esta última se implementa en un equipo cliente que ejecuta una versión anterior del cliente de Configuration Manager, entonces no podrá aplicarse. Actualizar estos clientes anteriores resolverá este problema. Todavía se pueden aplicar directivas que no engloban ninguna regla de inclusión en las versiones anteriores del cliente de Configuration Manager.

## <a name="how-to-deploy-a-device-guard-policy"></a>Implementación de una directiva de Device Guard
1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2.  En el área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y haga clic en **Directivas de Device Guard**.
3.  En la lista de directivas, seleccione la que quiera implementar y, después, en la pestaña **Inicio**, en el grupo **Implementación**, haga clic en **Implementar**.
4.  En el cuadro de diálogo **Implementar la directiva Device Guard**, seleccione la colección a la que desea implementar la directiva. A continuación, configure una programación para determinar cuándo los clientes evalúan la directiva. Por último, seleccione si el cliente puede evaluar la directiva fuera de las ventanas de mantenimiento configuradas.
5.  Cuando haya terminado, haga clic en **Aceptar** para implementar la directiva. 

Una vez se procese la directiva en un equipo cliente, se programa un reinicio en ese cliente según la opción **Configuración de cliente** para **Reinicio de equipo**.
La directiva no se aplica hasta que reinicie el equipo cliente.**

## <a name="how-to-monitor-a-device-guard-policy"></a>Supervisión de una directiva de Device Guard

Utilice la información del tema [Supervisión de la configuración de cumplimiento](/sccm/compliance/deploy-use/monitor-compliance-settings) a fin de poder supervisar que la directiva implementada se ha aplicado correctamente a todos los equipos.

Para supervisar el procesamiento de una directiva de Device Guard, utilice el siguiente archivo de registro en los equipos cliente:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Para comprobar el software específico que se bloquea o audita, vea los siguientes registros de eventos de cliente local:

1.  Para bloquear y auditar archivos ejecutables, utilice **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **Integridad de código** > **Operativo**.
2.  Para bloquear y auditar Windows Installer y archivos de script, utilice **Registros de aplicaciones y servicios** > **Microsoft** > **Windows** > **AppLocker** > **MSI y script**.

## <a name="security-and-privacy-information-for-device-guard"></a>Información de seguridad y privacidad para Device Guard

- En esta versión preliminar, no implemente directivas de Device Guard con el modo de cumplimiento **Solo auditoría** en un entorno de producción. Este modo está diseñado para ayudarle a probar la funcionalidad solo en una configuración de laboratorio.
- Los dispositivos que tienen una directiva implementada en el modo **Solo auditoría** o **Cumplimiento habilitado**, que no se han reiniciado para aplicar la directiva, son vulnerables al software que no es de confianza que se instala.
En esta situación, el software podría seguir teniendo permiso para ejecutarse incluso si se reinicia el dispositivo, o recibe una directiva en modo **Cumplimiento habilitado**.
- Para asegurarse de que la directiva de Device Guard es eficaz, prepare el dispositivo en un entorno de laboratorio. A continuación, implemente la directiva **Cumplimiento habilitado** y, por último, reinicie el dispositivo antes de enviar el dispositivo a un usuario final.
- No implemente una directiva con **Cumplimiento habilitado** y, a continuación, una directiva con **Solo auditoría** en el mismo dispositivo. Esta configuración puede provocar la ejecución de software que no es de confianza.
- Al utilizar Configuration Manager para habilitar la integridad de código configurable en los equipos cliente con las directivas de Device Guard, la directiva no evita que los usuarios con derechos de administrador local sorteen la directiva de Device Guard o ejecuten software que no es de confianza de otro modo. 
- La única manera de evitar que los usuarios con derechos de administrador local deshabiliten la integridad de código configurable es mediante la implementación de una directiva binaria firmada. Esta implementación es posible a través de la directiva de grupo, pero no se admite actualmente en Configuration Manager.
- La configuración de Configuration Manager como un instalador administrado en los equipos cliente utiliza la directiva de AppLocker. AppLocker solo se usa para identificar los instaladores administrados y todo el cumplimiento tiene lugar con la integridad de código configurable. 




