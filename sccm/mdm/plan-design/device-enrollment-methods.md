---
title: Métodos de inscripción de dispositivos para MDM híbrida
titleSuffix: Configuration Manager
description: Métodos de inscripción de dispositivos para MDM híbrida.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eda9de25d3bdb1a1563d8b74e78ddcad259683f6
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678726"
---
# <a name="overview-of-device-enrollment-methods"></a>Información general de los métodos de inscripción de dispositivos

*Se aplica a: System Center Configuration Manager (Rama actual)*

Tras extender Configuration Manager con Intune, puede inscribir y administrar dispositivos de propiedad corporativa o proporcionar permiso a los usuarios para inscribir sus dispositivos personales. También puede administrar dispositivos corporativos con Intune mediante Configuration Manager.

En la siguiente tabla se muestran los métodos de inscripción con las funcionalidades que se admiten. Estas funcionalidades incluyen:
- **Borrar**: restablecimiento de fábrica del dispositivo, borrando todos los datos. [Retirar dispositivos](../deploy-use/wipe-lock-reset-devices.md)
- **Afinidad**: asocia los dispositivos con los usuarios. Se requiere para la administración de aplicaciones móviles (MAM) y el acceso condicional a los datos de la compañía. [Afinidad de usuario](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Bloqueo**: evita que los usuarios quiten el dispositivo de la administración. Los dispositivos iOS requieren el modo supervisado para el bloqueo. [Bloqueo remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**Métodos de inscripción de iOS**

| **Método** | **Borrar** | **Afinidad** | **Bloqueo** | **Detalles** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No| Sí | No | [Más](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**| No |No |No | [Más](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**| Sí | Opcional | Opcional|[Más](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sí | Opcional | No| [Más](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de inscripción de Windows y Android**

| **Método** | **Borrar** | **Afinidad** | **Bloqueo** | **Detalles**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No| Sí | No | [Más](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**| No |No |No |[Más](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para obtener una serie de preguntas que pueden ayudarle a buscar el método correcto, consulte [Elegir cómo inscribir dispositivos móviles](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Los usuarios de "Bring Your Own Device" (BYOD) instalan la aplicación de portal de empresa e inscriben su dispositivo. Esto puede permitir a los usuarios conectarse a la red de la empresa, uniéndose al dominio o a Azure Active Directory. Habilitar la inscripción BYOD es un requisito previo de muchos escenarios COD para la mayoría de las plataformas. Consulte [Setup hybrid MDM (Configurar MDM híbrido)](../deploy-use/setup-hybrid-mdm.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos de propiedad corporativa
Los dispositivos de propiedad corporativa (COD) pueden administrarse con la consola de Configuration Manager. Los dispositivos iOS pueden inscribirse directamente mediante herramientas que proporciona Apple. Todos los tipos de dispositivos pueden inscribirse por un administrador mediante el administrador de inscripción de dispositivos. Los dispositivos con un número IMEI también pueden identificarse y etiquetarse como dispositivos de propiedad corporativa para habilitar escenarios COD.

[Inscribir dispositivos de propiedad corporativa](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
El administrador de la inscripción de dispositivos es una cuenta de usuario especial que se usa para inscribir y administrar varios dispositivos de propiedad corporativa. Los administradores pueden instalar el portal de empresa e inscribir muchos dispositivos sin usuario. Obtenga más información sobre [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
La administración del Programa de inscripción de dispositivos de Apple (DEP) le permite crear e implementar una directiva "mediante red inalámbrica" en los dispositivos iOS comprados y administrados con DEP. El dispositivo se inscribe cuando el usuario activa el dispositivo por primera vez y ejecuta el asistente de configuración de iOS. Este método admite el modo **supervisado de iOS** que a su vez habilita:
  - Inscripción bloqueada
  - Acceso condicional
  - Detección de Jailbreak
  - Administración de aplicaciones móviles

Obtenga más información sobre [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Inscripción con el asistente de configuración conectado por USB. El administrador crea una directiva y la exporta a Apple Configurator. Los dispositivos de propiedad corporativa conectados por USB se preparan con la directiva. El administrador debe inscribir cada dispositivo manualmente. Los usuarios reciben sus dispositivos y ejecutan el asistente de configuración inscribiendo su dispositivo. Este método admite el modo **supervisado de iOS** que a su vez habilita:
  - Acceso condicional
  - Detección de Jailbreak
  - Administración de aplicaciones móviles

Obtenga más información sobre [Setup Assistant enrollment with Apple Configurator (Inscripción del asistente de configuración con Apple Configurator)](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Administración de dispositivos móviles con Exchange ActiveSync y Configuration Manager
Los dispositivos móviles que no están inscritos pero que se conectan a Exchange ActiveSync (EAS) pueden administrarse mediante Intune con la directiva MDM de EAS. Intune usa un conector de Exchange para comunicarse con EAS, de manera local y hospedado en la nube.

[Administración de dispositivos móviles con Exchange ActiveSync e Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
