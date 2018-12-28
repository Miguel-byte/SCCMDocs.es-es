---
title: Configuración de MDM híbrida
titleSuffix: Configuration Manager
description: Configure la inscripción de dispositivos híbridos con Configuration Manager e Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a69f849d4843ff7a0cf7df4a0b6de044a9506301
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421814"
---
# <a name="set-up-hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Configure MDM híbrida con Configuration Manager y Microsoft Intune.

*Se aplica a: System Center Configuration Manager (rama actual)*


Para poder administrar dispositivos iOS, Windows y Android con Configuration Manager, deben estar inscritos con Intune. Siga estos pasos para configurar la inscripción de dispositivos híbridos con Configuration Manager mediante Intune. Al completar los pasos siguientes, habilitará la inscripción "Bring Your Own Device" (BYOD) para los usuarios. Estos pasos son también requisitos previos para [inscribir dispositivos BYOD](enroll-hybrid-ios-mac.md) e [inscribir dispositivos propiedad de la empresa](enroll-company-owned-devices.md).

> [!Important]  
> Desde el 14 de agosto de 2018, la administración híbrida de dispositivos móviles es una [característica en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->  



## <a name="set-up-steps"></a>Pasos de configuración

 |Pasos|Detalles|  
 |-----------|-------------|  
 |**Paso 1:** [Crear una recopilación de MDM](create-mdm-collection.md)|Crear una recopilación de usuarios de Configuration Manager con los usuarios que pueden inscribir sus dispositivos|  
 |**Paso 2:** [Requisitos de nombre de dominio](confirm-dns.md)|Confirmar que la administración de usuarios de Active Directory y el servicio de nombres de dominio (DNS) de su organización cumple los requisitos de MDM|
 |**Paso 3:** [Configurar la suscripción a Intune](configure-intune-subscription.md)|El servicio de Intune le permite administrar dispositivos a través de Internet.|  
 |**Paso 4:** [Agregar términos y condiciones](terms-and-conditions.md)| Crear términos y condiciones que deben aceptar los usuarios para poder usar la aplicación Portal de empresa|
 |**Paso 5:** [Crear el punto de conexión de servicio](create-service-connection-point.md)|El punto de conexión de servicio envía información de configuración e implementación de software a Configuration Manager y recupera mensajes de inventario y estado de dispositivos móviles. |  
 |**Paso 6:** [Habilitar la inscripción de plataforma](enable-platform-enrollment.md)|La inscripción de MDM para dispositivos iOS y Windows requiere pasos adicionales para la comunicación entre los servicios y dispositivos. Android no requiere ninguna configuración adicional.|  
 |**Paso 7:** [Configurar la administración adicional](set-up-additional-management.md)|(Opcional) Configurar los elementos de configuración y de acceso condicional para dispositivos inscritos|
 |**Paso 8:** [Comprobar la configuración de MDM](verify-mdm-configuration.md)|Ver los archivos de registro para confirmar que el punto de conexión de servicio se ha creado correctamente y las cuentas de usuario se sincronizan.|



## <a name="enroll-devices"></a>Inscribir dispositivos

Una vez completada la configuración híbrida, se pueden inscribir dispositivos en Configuration Manager de varias maneras:

- **Dispositivos corporativos (COD):** [Inscribir dispositivos propiedad de la empresa](enroll-company-owned-devices.md) proporciona orientación sobre las diferentes formas específicas de la plataforma para inscribir dispositivos propiedad de la empresa  

- **Dispositivos propiedad del usuario (BYOD):** [Inscribir dispositivos propiedad del usuario (BYOD)](enroll-hybrid-ios-mac.md) se proporcionan instrucciones sobre cómo inscribir dispositivos propiedad del usuario  



## <a name="see-also"></a>Consulte también

¿Busca Intune sin Configuration Manager?
> [!div class="button"]
> [Ver documentos de Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


