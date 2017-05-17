---
title: "Configurar la MDM híbrida | Microsoft Docs"
description: "Configure la inscripción de dispositivos híbridos con Configuration Manager e Intune."
ms.custom: na
ms.date: 03/05/2017
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
author: mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurar la administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*


Para poder administrar dispositivos iOS, Windows y Android con Configuration Manager, deben estar inscritos con Intune. Use los pasos siguientes para configurar la inscripción de dispositivos híbridos con Configuration Manager mediante Intune. Al completar los pasos siguientes, habilitará la inscripción "Bring Your Own Device" (BYOD) para los usuarios. Estos pasos son también requisitos previos para [inscribir dispositivos BYOD](enroll-hybrid-ios-mac.md) e [inscribir dispositivos propiedad de la empresa](enroll-company-owned-devices.md).

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

¿Busca Intune sin Configuration Manager?
> [!div class="button"]
[Ver documentos de Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Inscribir dispositivos
Una vez completada la configuración híbrida, se pueden inscribir dispositivos en Configuration Manager de varias maneras:
- **Dispositivos propiedad de la empresa (COD):** [la inscripción de dispositivos propiedad de la empresa](enroll-company-owned-devices.md) proporciona directrices sobre las diferentes formas específicas de la plataforma de inscribir dispositivos propiedad de la empresa.
- **Dispositivos propiedad del usuario (BYOD):** [la inscripción de dispositivos propiedad del usuario (BYOD)](enroll-hybrid-ios-mac.md) proporciona instrucciones sobre las formas de inscribir dispositivos propiedad del usuario.

