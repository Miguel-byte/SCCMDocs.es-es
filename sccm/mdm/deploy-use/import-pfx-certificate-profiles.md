---
title: "Creación de perfiles de certificado PFX mediante la importación de detalles de certificado"
titleSuffix: Configuration Manager
description: "Obtenga información sobre cómo usar archivos PFX en System Center Configuration Manager para generar certificados específicos del usuario que admiten el intercambio de datos cifrados."
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 
caps.handback.revision: 
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 25c6927698e409ff3b0c3f846e2cc567a6f458ab
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Creación de perfiles de certificado PFX mediante la importación de detalles de certificado.

*Se aplica a: System Center Configuration Manager (rama actual)*


A continuación, aprenderá a crear un perfil de certificado mediante la importación de credenciales de certificados externos.  

Los [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) proporcionan información general sobre la creación y configuración de perfiles de certificado. En este tema se destaca información específica sobre perfiles de certificado relacionados con certificados PFX.

-  Configuration Manager admite diversos almacenes de certificados adecuados para diferentes dispositivos y sistemas operativos.  Entre ellos, se incluye:

 -   iOS y macOS/OSX
 -   Android y Android for Work
 -   Windows 10, incluidos Windows 10 Mobile

Para obtener más información, consulte [Requisitos previos de los perfiles de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfiles de certificado PFX
System Center Configuration Manager permite importar y, luego, aprovisionar archivos de intercambio de información personal (.pfx) en los dispositivos de usuario. Los archivos PFX pueden usarse para generar certificados específicos del usuario para admitir el intercambio de datos cifrados.

> [!TIP]  
>  En [Cómo crear e implementar perfiles de certificado PFX en Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)también encontrará un tutorial detallado en el que se describe este proceso.  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creación, importación e implementación de un perfil de certificado de intercambio de información personal (PFX)  

### <a name="get-started"></a>Introducción

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  
2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de certificado**.  

3.  En la pestaña **Inicio** del grupo **Crear** , haga clic en **Crear perfil de certificado**.

4.  En la página **General** del asistente para **Crear perfil de certificado** , especifique la información siguiente:  

    -   **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    -   **Descripción**: facilite una descripción general del perfil de certificado y cualquier otra información adicional pertinente para identificarlo en la consola de System Center Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

    -   **Especifique el tipo de perfil de certificado que desea crear.**: para los certificados PFX, elija una de las siguientes opciones:  

        -   **Intercambio de información personal: configuración de PKCS #12 (PFX): importar**: crea un perfil de certificado importando mediante programación información de certificados existentes.  

        -   **Intercambio de información personal -- Configuración de PKCS #12 (PFX) -- Crear**: crea un perfil de certificado PFX mediante credenciales que proporcione una entidad de certificación.  Para obtener más información, consulte [Creación de perfiles de certificado PFX mediante una entidad de certificación](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Creación de un perfil de certificado PFX para las credenciales importadas

Para importar un certificado PFX, se utiliza el SDK de Configuration Manager para implementar un script de creación de PFX. 

Más adelante, los certificados importados se implementan en los dispositivos inscritos.

1. En la página **Certificado PFX** del **Asistente para crear perfil de certificado**, especifique dónde se instalará el proveedor de almacenamiento de claves de dispositivo:
    -   **Instalar en Módulo de plataforma segura (TPM) si está presente**  
    -   **Instalar en Módulo de plataforma segura (TPM) o se producirá un error** 
    -   **Instalar en Windows Hello para empresas o generar un error** 
    -   **Instalar en Proveedor de almacenamiento de claves de software** 
2. Haga clic en **Siguiente**. 
3. En la página **Plataformas admitida** del asistente, seleccione las plataformas de dispositivo admitidas donde se instalará este certificado y, luego, haga clic en **Siguiente**.

### <a name="finish-the-profile"></a>Finalización del perfil

1.  Haga clic en **Siguiente**, revise la página **Resumen** y cierre el asistente.  
2.  El perfil de certificado que contiene el archivo PFX ya está disponible en el área de trabajo **Perfiles de certificado** . 
3.  Para implementar el perfil, en el área de trabajo **Activos y compatibilidad**, abra **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de certificado**, haga clic con el botón derecho en el certificado deseado y luego haga clic en **Implementar**. 

### <a name="deploy-a-create-pfx-script"></a>Implementación de un script de creación de PFX

Use el [SDK de Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=613525) para implementar un script de creación de PFX. 

El script de creación de PFX agregado en Configuration Manager 2012 SP2 agrega una clase SMS_ClientPfxCertificate al SDK. Esta clase incluye los métodos siguientes:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

En el ejemplo siguiente se importan las credenciales en un perfil de certificado PFX.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

Para usar este ejemplo, actualice las siguientes variables de script:  

   -   **blob**\: blob cifrado en base 64 de PFX  
   -   **$Password**: contraseña del archivo PFX  
   -   **$ProfileName** nombre del perfil PFX  
   -   **ComputerName** nombre del equipo host   

## <a name="see-also"></a>Consulte también
[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md) le guiará a través del Asistente para crear perfil de certificado.

[Creación de perfiles de certificado PFX mediante la importación de detalles de certificado](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

[Implementación de perfiles de Wi-Fi, VPN, correo electrónico y certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) describe cómo implementar perfiles de certificado.