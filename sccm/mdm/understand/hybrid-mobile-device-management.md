---
title: Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune
description: "Obtenga información sobre la administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 22e673122f0f664d1240c11451b7e6db78481b26
ms.openlocfilehash: 83832465e93997a2893e024c565ee00f471036d1

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*


Puede administrar dispositivos iOS, Windows y Android con Configuration Manager y Microsoft Intune. Todas las tareas de administración se controlan desde la consola de Configuration Manager donde realiza el resto de las tareas de administración que se integran perfectamente al servicio en línea de Microsoft Intune mediante Internet.  Puede usar Configuration Manager para permitir a los usuarios un acceso seguro y administrado a los recursos de la compañía en sus dispositivos. Mediante el uso de la administración de dispositivos, se protegen los datos de la compañía a la vez que se permite a los usuarios inscribir sus dispositivos corporativos o personales para tener acceso a los datos de la compañía. Funcionalidades de administración en dispositivos:

-   Retirar y borrar dispositivos
-   Definir la configuración de cumplimiento, como contraseñas, seguridad, movilidad, cifrado y comunicación inalámbrica
-   Implementar aplicaciones de línea de negocio (LOB) en los dispositivos
-   Implementar aplicaciones en los dispositivos que se conectan a la Tienda Windows, la Tienda Windows Phone, App Store o Google Play
-   Recopilar información de inventario de hardware
-   Recopilar información de inventario de software mediante el uso de informes integrados

Para leer sobre las nuevas características que están disponibles para MDM híbrido, consulte [What's new in hybrid mobile device management (Novedades en la administración híbrida de dispositivos móviles)](../understand/whats-new-in-hybrid-mobile-device-management.md).

En este documento se supone que usa Configuration Manager para administrar equipos y que quiere extender la consola de Configuration Manager con Intune para administrar dispositivos móviles. Para comprender las diferencias entre Intune y la administración híbrida de dispositivos móviles, consulte [Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager (Elección entre Microsoft Intune independiente y la administración híbrida de dispositivos móviles con System Center Configuration Manager)](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Tras extender Configuration Manager con Intune, puede inscribir y administrar dispositivos de propiedad corporativa o proporcionar permiso a los usuarios para inscribir sus dispositivos personales. También puede administrar dispositivos corporativos con Intune mediante Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscripción híbrida de MDM
Para integrar dispositivos en la administración híbrida, esos dispositivos deben inscribirse al servicio. La manera en que los dispositivos inscriben dispositivos depende del tipo de dispositivo, la propiedad y el nivel de administración necesario. La inscripción "Bring Your Own Device" (BYOD) permite a los usuarios inscribir sus teléfonos personales, tabletas o equipos PC. La inscripción de dispositivos de propiedad corporativa (COD) habilita la administración de escenarios como el borrado remoto, los dispositivos compartidos o la afinidad de usuario para un dispositivo.

 Si usa [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager), de manera local u hospedado en la nube, puede habilitar la administración simple de Intune sin la inscripción. Los equipos con Windows también pueden administrarse mediante el [software cliente de Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

## <a name="overview-of-device-enrollment-methods"></a>Información general de los métodos de inscripción de dispositivos

 En la siguiente tabla se muestran los métodos de inscripción con las funcionalidades que se admiten. Estas funcionalidades incluyen:
 - **Borrar**: restablecimiento de fábrica del dispositivo, borrando todos los datos. [Retirar dispositivos](../deploy-use/wipe-lock-reset-devices.md)
 - **Afinidad**: asocia los dispositivos con los usuarios. Se requiere para la administración de aplicaciones móviles (MAM) y el acceso condicional a los datos de la compañía. [Afinidad de usuario](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Bloqueo**: evita que los usuarios quiten el dispositivo de la administración. Los dispositivos iOS requieren el modo supervisado para el bloqueo. [Bloqueo remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **Métodos de inscripción de iOS**

| **Método** |  **Borrar** |  **Afinidad**    |   **Bloqueo** | **Detalles** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Sí |   No | [Más](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   No |No |No  | [Más](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sí |   Opcional |  Opcional|[Más](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sí |   Opcional |  No| [Más](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Métodos de inscripción de Windows y Android**

| **Método** |  **Borrar** |  **Afinidad**    |   **Bloqueo** | **Detalles**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Sí |   No | [Más](../deploy-use/setup-hybrid-mdm.md#set-up-device-management)|
|**[DEM](#dem)**|   No |No |No  |[Más](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Para obtener una serie de preguntas que pueden ayudarle a buscar el método correcto, consulte [Elegir cómo inscribir dispositivos móviles](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Los usuarios de "Bring Your Own Device" instalan la aplicación de portal de empresa e inscriben su dispositivo. Esto puede permitir a los usuarios conectarse a la red de la empresa, uniéndose al dominio o a Azure Active Directory. Habilitar la inscripción BYOD es un requisito previo de muchos escenarios COD para la mayoría de las plataformas. Consulte [Setup hybrid MDM (Configurar MDM híbrido)](../deploy-use/setup-hybrid-mdm.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivos de propiedad corporativa
Los dispositivos de propiedad corporativa (COD) pueden administrarse con la consola de Configuration Manager. Los dispositivos iOS pueden inscribirse directamente mediante herramientas que proporciona Apple. Todos los tipos de dispositivos pueden inscribirse por un administrador mediante el administrador de inscripción de dispositivos. Los dispositivos con un número IMEI también pueden identificarse y etiquetarse como dispositivos de propiedad corporativa para habilitar escenarios COD.

[Inscribir dispositivos de propiedad corporativa](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
El administrador de la inscripción de dispositivos es una cuenta de usuario especial que se usa para inscribir y administrar varios dispositivos de propiedad corporativa. Los administradores pueden instalar el portal de empresa e inscribir muchos dispositivos sin usuario. Obtenga más información sobre [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
La administración del Programa de inscripción de dispositivos de Apple (DEP) le permite crear e implementar una directiva "mediante red inalámbrica" en los dispositivos iOS comprados y administrados con DEP. El dispositivo se inscribe cuando el usuario activa el dispositivo por primera vez y ejecuta el asistente de configuración de iOS. Este método admite el modo **supervisado de iOS** que a su vez habilita:
   -    Inscripción bloqueada
   -    Acceso condicional
   -    Detección de Jailbreak
   -    Administración de aplicaciones móviles

Obtenga más información sobre [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Inscripción con el asistente de configuración conectado por USB. El administrador crea una directiva y la exporta a Apple Configurator. Los dispositivos de propiedad corporativa conectados por USB se preparan con la directiva. El administrador debe inscribir cada dispositivo manualmente. Los usuarios reciben sus dispositivos y ejecutan el asistente de configuración inscribiendo su dispositivo. Este método admite el modo **supervisado de iOS** que a su vez habilita:
   -    Acceso condicional
   -    Detección de Jailbreak
   -    Administración de aplicaciones móviles

Obtenga más información sobre [Setup Assistant enrollment with Apple Configurator (Inscripción del asistente de configuración con Apple Configurator)](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Volver a la tabla](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Administración de dispositivos móviles con Exchange ActiveSync y Configuration Manager
Los dispositivos móviles que no están inscritos pero que se conectan a Exchange ActiveSync (EAS) pueden administrarse mediante Intune con la directiva MDM de EAS. Intune usa un conector de Exchange para comunicarse con EAS, de manera local y hospedado en la nube.

[Administración de dispositivos móviles con Exchange ActiveSync e Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)


##  <a name="supported-device-platforms"></a>Plataformas de dispositivos compatibles

MDM híbrido de Configuration Manager puede administrar las siguientes plataformas de dispositivos:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>Pasos siguientes
 - [Requisitos previos para la inscripción de dispositivos](../deploy-use/setup-hybrid-mdm.md)
 - [Administrar dispositivos de propiedad corporativa](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Nov16_HO1-->


