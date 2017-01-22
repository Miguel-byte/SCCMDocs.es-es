---
title: "Configuración de la administración de dispositivos híbrida de iOS y Mac con System Center Configuration Manager y Microsoft Intune | Microsoft Docs"
description: "Configure la administración de dispositivos de iOS con System Center Configuration Manager y Microsoft Intune."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 74c75653e69154ced18d5bc713b1d9b89e88ae64


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configuración de la administración de dispositivos híbrida de iOS con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (rama actual)*

Con Configuration Manager e Intune, puede habilitar la inscripción BYOD ("Bring Your Own Device") de dispositivos iOS y Mac OS X para proporcionar acceso al correo electrónico y a los recursos de la empresa a los usuarios de iPhone, iPad y Mac. Una vez que los usuarios instalen la aplicación del portal de empresa Intune, puede aplicar directivas a sus dispositivos. Antes de que pueda administrar dispositivos iOS y Mac, debe importar un certificado del Servicio de notificaciones push de Apple (APNs). Este certificado permite a Intune administrar dispositivos iOS y Mac, además de establecer una conexión de IP acreditada y cifrada con los servicios de entidad de administración de dispositivos móviles.  

 También puede inscribir dispositivos iOS de empresa.  Consulte [Enroll company-owned devices](enroll-company-owned-devices.md) (Inscripción de dispositivos de empresa).  

## <a name="enable-ios-device-enrollment"></a>Habilitar la inscripción de dispositivos iOS  
 Para permitir la inscripción de dispositivos iOS, debe seguir estos pasos:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Configurar la inscripción de dispositivos iOS en Configuration Manager  

1.  **Requisitos previos**: para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de [Setup hybrid MDM](setup-hybrid-mdm.md) (Configurar la MDM híbrida).    

2.  **Descargue una solicitud de firma de certificado** : se necesita un archivo de solicitud de firma de certificado (.csr) para solicitar un certificado de APNs de Apple.  

    1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube**> **Suscripciones a Microsoft Intune**.  

    2.  En la pestaña **Inicio** , haga clic en **Crear solicitud de certificado APN**. Se abre el cuadro de diálogo **Solicitar petición de firma de certificado de servicio de notificaciones push de Apple** .  

    3.  Utilice la función**Examinar** para seleccionar la ruta de acceso donde se guardará el nuevo archivo de solicitud de firma de certificado (.csr). Guarde la solicitud de firma de certificado (.csr) en el equipo local.  

    4.  Haga clic en **Descargar**. El nuevo archivo .csr de Microsoft Intune se descarga y Configuration Manager lo guarda. Se utiliza el archivo .csr para solicitar un certificado de relación de confianza desde el portal de certificados push de Apple.  

3.  **Solicite un certificado de APNs de Apple** : el certificado del Servicio de notificaciones push Apple (APNs) se usa para establecer una relación de confianza entre el servicio de administración, Intune y los dispositivos móviles iOS inscritos.  

    1.  En un explorador, vaya al [portal de certificados push de Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con su identificador de Apple de empresa. Este ID de Apple debe utilizarse en el futuro para renovar el certificado APNs.  

    2.  Complete el asistente usando el archivo de solicitud de firma de certificado (.csr). Descargue el certificado de APNs y guarde el archivo .pem localmente. Este archivo de certificado de APNs (.pem) se usa para establecer una relación de confianza entre el servidor de notificaciones push de Apple y la entidad de administración de dispositivos móviles de Intune.  

4.  **Habilite la inscripción y cargue el certificado de APNs** : para habilitar la inscripción de iOS, cargue el certificado de APNs.  

    1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.  

    2.  En la pestaña **Inicio** en el grupo **Suscripción** , haga clic en **Configurar plataformas** > **IOS**.  

        > [!NOTE]  
        >  No cargue el certificado del Servicio de notificaciones push de Apple (APNs) hasta que habilite la inscripción de iOS en la consola de Configuration Manager.  

    3.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune** , seleccione la pestaña **iOS** y haga clic para seleccionar la casilla **Habilitar la inscripción de iOS** .  

    4.  Haga clic en **Examinar**y vaya al archivo de certificado de APNs (.cer) que descargó de Apple. Manager Configuration muestra la información del certificado de APNs. Haga clic en **Aceptar** para guardar en Intune el certificado de APNs.  

 Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.



<!--HONumber=Dec16_HO3-->


