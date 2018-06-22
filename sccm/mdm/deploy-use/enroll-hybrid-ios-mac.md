---
title: Configuración de la administración de dispositivos híbridos Mac e iOS con Microsoft Intune
titleSuffix: Configuration Manager
description: Configure la administración de dispositivos de iOS con System Center Configuration Manager y Microsoft Intune.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9407180df12902c17f4de8e52be13229ce35c60b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348834"
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configuración de la administración de dispositivos híbrida de iOS con System Center Configuration Manager y Microsoft Intune

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con Configuration Manager e Intune, puede habilitar la inscripción de dispositivos iOS y macOS para proporcionar acceso al correo electrónico y a los recursos de la empresa a los usuarios de iPhone, iPad y Mac. Una vez que los usuarios instalen la aplicación del portal de empresa Intune, puede aplicar directivas a sus dispositivos. Antes de que pueda administrar dispositivos iOS y Mac, debe importar un certificado del Servicio de notificaciones push de Apple (APNs). Este certificado permite a Intune administrar dispositivos iOS y Mac mediante el establecimiento de una conexión con el servicio de administración de dispositivos de Apple.  

 También puede inscribir dispositivos iOS de empresa.  Consulte [Enroll company-owned devices](enroll-company-owned-devices.md) (Inscripción de dispositivos de empresa).  

**Requisitos previos**<br>
Para poder configurar la inscripción en cualquier plataforma, complete los requisitos previos y los procedimientos de la sección sobre cómo [configurar la MDM híbrida](setup-hybrid-mdm.md).

Para permitir la inscripción de dispositivos iOS, debe seguir estos pasos:  

## <a name="download-a-certificate-signing-request"></a>Descarga de una solicitud de firma de certificado
Se necesita un archivo de solicitud de firma de certificado para solicitar un certificado de APNs de Apple.  

1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube**> **Suscripciones a Microsoft Intune**.  

2.  En la pestaña **Inicio** , haga clic en **Crear solicitud de certificado APN**. Se abre el cuadro de diálogo **Solicitar petición de firma de certificado de servicio de notificaciones push de Apple** .  

3.  Utilice la función**Examinar** para seleccionar la ruta de acceso donde se guardará el nuevo archivo de solicitud de firma de certificado. Guarde la solicitud de firma de certificado en el equipo local.  

4.  Haga clic en **Descargar**. El nuevo archivo de solicitud de firma de certificado de Microsoft Intune se descarga y Configuration Manager lo guarda. El archivo de solicitud de firma de certificado se utiliza para solicitar un certificado de relación de confianza desde el portal Apple Push Certificates Portal.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Solicitud de un certificado push MDM de Apple
El certificado push MDM se usa para establecer una relación de confianza entre el servicio de administración, Intune y los dispositivos móviles iOS inscritos.  

1.  En un explorador, vaya al [portal de certificados push de Apple](http://go.microsoft.com/fwlink/?LinkId=269844) e inicie sesión con su identificador de Apple de empresa. Este ID de Apple debe utilizarse en el futuro para renovar el certificado APNs.  

2.  Complete el asistente usando el archivo de solicitud de firma de certificado (.csr). Descargue el certificado push de MDM y guarde el archivo .pem de forma local. Este archivo de certificado (.pem) se usa para establecer una relación de confianza entre el servidor de notificaciones push de Apple y la entidad de administración de dispositivos móviles de Intune.  

> [!NOTE]  
>  No cargue el certificado de Apple Push Notification Service(APNs) hasta que habilite la inscripción de iOS en la consola de Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Habilitación de la inscripción y carga del certificado push de MDM
Para habilitar la inscripción de iOS, cargue el certificado de APNs.  

1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.  

2.  En la pestaña **Inicio** en el grupo **Suscripción** , haga clic en **Configurar plataformas** > **IOS**.  

3.  En el cuadro de diálogo **Propiedades de suscripción a Microsoft Intune** , seleccione la pestaña **iOS** y haga clic para seleccionar la casilla **Habilitar la inscripción de iOS** .  
4.  Haga clic en **Examinar**y vaya al archivo de certificado de APNs (.cer) que descargó de Apple. Manager Configuration muestra la información del certificado de APNs. Haga clic en **Aceptar** para guardar en Intune el certificado de APNs.  

Cuando esté listo, necesitará que los usuarios sepan cómo inscribir sus dispositivos. Consulte [Qué decirles a los usuarios finales sobre el uso de Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate). Esta información se aplica a Microsoft Intune y a dispositivos móviles administrados por Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configuración de restricciones de inscripción

Puede limitar los dispositivos que se pueden inscribir bloqueando dispositivos de propiedad personal. Esto impide que los usuarios inscriban sus dispositivos a través del Portal de empresa. Si bloquea los dispositivos de propiedad personal, solo se pueden inscribir los siguientes dispositivos:
- [Dispositivos predeclarados](predeclare-devices-with-hardware-id.md)
- [Dispositivos administrados con Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md)
- [Dispositivos administrados con el Programa de inscripción de dispositivos (DEP)](ios-device-enrollment-program-for-hybrid.md)
- Dispositivos inscritos con una [cuenta del administrador de inscripciones de dispositivos](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Para habilitar las restricciones de inscripción
1.  En la consola de Configuration Manager, en el área de trabajo **Administración** , vaya a **Servicios en la nube** > **Suscripción a Microsoft Intune**.
2.  En la pestaña **Inicio** en el grupo **Suscripción** , haga clic en **Configurar plataformas** > **IOS**.
3.  Elija **Bloquear dispositivos de propiedad personal** para limitar la inscripción a dispositivos que son propiedad de la empresa.

> [!div class="button"]
[< Paso anterior](create-service-connection-point.md)  [Paso siguiente >](set-up-additional-management.md)
