---
title: Administración del bloqueo de activación de iOS
titleSuffix: Configuration Manager
description: Administre el bloqueo de activación de iOS con System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8a695a0b777f4adf3d2fb336df6aced8702e9dab
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125262"
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Administración del bloqueo de activación de iOS con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*


System Center Configuration Manager puede ayudarle a administrar el bloqueo de activación de iOS, una característica de la aplicación Buscar mi iPhone disponible en iOS 7.1 y en dispositivos más modernos. Cuando el bloqueo de activación está habilitado, es necesario escribir el identificador y la contraseña de Apple del usuario antes de que se pueda:

- Desactivar Buscar mi iPhone
- Borrar el dispositivo
- Reactivar el dispositivo

En los dispositivos **sin supervisar** , el bloqueo de activación se habilita automáticamente cuando se utiliza la aplicación Buscar mi iPhone.

En los dispositivos **supervisados** , debe activarse mediante la configuración de cumplimiento de Configuration Manager.

> [!TIP]
> El modo supervisado de los dispositivos iOS permite usar la herramienta Apple Configurator para bloquear un dispositivo a fin de limitar la funcionalidad para fines empresariales específicos. Generalmente, el modo supervisado es solo para los dispositivos de la empresa.

Aunque el bloqueo de activación ayuda a proteger dispositivos iOS y aumenta las posibilidades de recuperarlos ante la pérdida o el robo, esta funcionalidad puede suponerle una serie de desafíos como administrador de TI. Por ejemplo:

- Uno de los usuarios establece el bloqueo de activación en un dispositivo. Luego, el usuario se va de la empresa y devuelve el dispositivo. Sin el identificador y la contraseña de Apple, no se puede reactivar el dispositivo, aunque se borre.
- Necesita un informe de todos los dispositivos que tienen habilitado el bloqueo de activación.
- Durante una actualización de los dispositivos de la organización, puede que desee reasignar algunos dispositivos a un departamento diferente. Solo puede volver a asignar dispositivos que no tengan habilitado el bloqueo de activación.


Para ayudar a resolver estos problemas, Apple incorporó el bypass del bloqueo de activación en iOS 7.1. Esto permite quitar el bloqueo de activación de los dispositivos supervisados sin el identificador y la contraseña de Apple del usuario. Los dispositivos supervisados pueden generar un código de bypass del bloqueo de activación específico del dispositivo, que se almacena en el servidor de activación de Apple.

[Aquí](https://support.apple.com/HT201365)encontrará más información sobre el bloqueo de activación.

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Cómo ayuda Configuration Manager a administrar el bloqueo de activación

Configuration Manager puede ayudarle a administrar el bloqueo de activación de dos formas:

1. Habilitando el bloqueo de activación en los dispositivos supervisados.
2. Omitiendo el bloqueo de activación en los dispositivos supervisados.

> [!IMPORTANT]
> El bloqueo de activación no se puede omitir en los dispositivos sin supervisar.

Esto brinda algunas ventajas a las empresas que tienen estos dispositivos:



- El usuario obtiene los beneficios de seguridad de la aplicación Buscar mi iPhone
- Puede permitir que el usuario haga su trabajo sabiendo que, cuando el dispositivo se deba reasignar, podrá retirarlo o desbloquearlo.


## <a name="enable-activation-lock-on-supervised-devices"></a>Habilitación del bloqueo de activación en los dispositivos supervisados

Puede utilizar la configuración de compatibilidad de Configuration Manager para crear e implementar un elemento de configuración de tipo **iOS y Mac OS X** a fin de habilitar el bloqueo de activación en dispositivos supervisados:

1. Utilice la información del tema [How to create configuration items for iOS and Mac OS X devices managed without the System Center Configuration Manager client](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) (Creación de elementos de configuración para dispositivos iOS y Mac OS X sin el cliente de System Center Configuration Manager) para crear un elemento de configuración de tipo **iOS y Mac OS X**.
2. En la página **Seguridad del sistema** del Asistente para crear elemento de configuración, establezca la opción **Allow Activation Lock (supervised mode only)** [Permitir bloqueo de activación (solo en modo supervisado)] en **Permitido**.
3. [Agregue el elemento de configuración a una línea base de configuración](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Implemente esta línea base de configuración](/sccm/compliance/deploy-use/deploy-configuration-baselines) en una recopilación que contenga los dispositivos iOS en los que desea habilitar el bloqueo de activación.

> [!IMPORTANT]
> Para seguir este procedimiento, debe tener el dispositivo físicamente. De lo contrario, el bloqueo de activación se omitirá y la persona que tenga el dispositivo tendrá acceso completo a él, lo que le permitirá desactivar la aplicación Buscar mi iPhone, borrar el dispositivo o reactivarlo.

Solo se puede omitir el bloqueo de activación o recuperar el código de omisión en los dispositivos supervisados. Si intenta omitir el bloqueo de activación en un dispositivo sin supervisar o ver el código de omisión, se producirá un error.



## <a name="view-the-activation-lock-bypass-code"></a>Visualización de código de omisión del bloqueo de activación

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos**.
3. Seleccione un dispositivo inscrito que esté en modo supervisado y que tenga el bloqueo de activación habilitado.
4. En la pestaña **Inicio** , en el grupo **Dispositivo** , haga clic en **Acciones de dispositivo remoto** > **View Activation Lock Bypass Code**(Ver código de omisión de bloqueo de activación).
5. En el cuadro de diálogo **Activation Lock Bypass Code** (Código de omisión de bloqueo de activación) aparecerá el código de omisión del dispositivo seleccionado.

## <a name="bypass-activation-lock"></a>Omisión del bloqueo de activación

1. En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad** , haga clic en **Dispositivos**.
3. Seleccione un dispositivo inscrito que esté en modo supervisado y que tenga el bloqueo de activación habilitado.
3. En la pestaña **Inicio** , en el grupo **Dispositivos** , haga clic en **Acciones de dispositivo remoto** > **Bypass Activation Lock**(Omitir bloqueo de activación).
5. Lea los mensajes de advertencia del cuadro de diálogo y haga clic en **Sí** cuando esté listo para continuar.
6. Puede ver el estado de la solicitud de desbloqueo en:

    - Los datos de detección del dispositivo, que aparecen en el cuadro de diálogo de propiedades del dispositivo.
    - La columna **Activation Lock Bypass State** (Estado de omisión de bloqueo de activación) de la vista **Dispositivos** (esta columna está oculta de forma predeterminada).
    - La sección **Remote Device Actions Information** (Información de acciones de dispositivo remoto) de la pestaña **Resumen** del panel de detalles (cuando hay un dispositivo seleccionado).
