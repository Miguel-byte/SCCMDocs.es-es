---
title: Crear perfiles de certificado PFX | Microsoft Docs
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
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 26feb0b166beb7e48cb800a5077d00dbc3eec51a
ms.openlocfilehash: 27435316c6e47531ff989bc8956ca0c874131a0e
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de certificados PFX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de certificado trabajan con los Servicios de certificados de Active Directory y el rol Servicio de inscripción de dispositivos de red para aprovisionar certificados de autenticación para dispositivos administrados para que los usuarios puedan acceder sin problemas a los recursos de empresa. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios inicien conexiones VPN e inalámbricas.

Los [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) proporcionan información general sobre la creación y configuración de perfiles de certificado. En este tema se destaca información específica sobre perfiles de certificado relacionados con certificados PFX.

-  Configuration Manager admite la implementación de certificados en varios almacenes de certificados distintos en función de los requisitos, el tipo de dispositivo y el sistema operativo. Cuando están inscritos con Intune, se admiten los siguientes dispositivos:

 -   iOS  

- Para información sobre otros requisitos previos, consulte [Requisitos previos de perfiles de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfiles de certificado PFX
System Center Configuration Manager permite importar y, luego, aprovisionar archivos de intercambio de información personal (.pfx) en los dispositivos de usuario. Los archivos PFX pueden usarse para generar certificados específicos del usuario para admitir el intercambio de datos cifrados.

> [!TIP]  
>  En [Cómo crear e implementar perfiles de certificado PFX en Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)también encontrará un tutorial detallado en el que se describe este proceso.  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creación e implementación de un perfil de certificado de intercambio de información personal (PFX)  

### <a name="get-started"></a>Introducción

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de certificado**.  

3.  En la pestaña **Inicio** del grupo **Crear** , haga clic en **Crear perfil de certificado**.

4.  En la página **General** del asistente para **Crear perfil de certificado** , especifique la información siguiente:  

    -   **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    -   **Descripción**: facilite una descripción general del perfil de certificado y cualquier otra información adicional pertinente para identificarlo en la consola de System Center Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

    -   **Especifique el tipo de perfil de certificado que desea crear**: para los certificados PF, elija:  

        -   **Intercambio de información personal: configuración de PKCS #12 (PFX): importar**: seleccione esta opción para importar un certificado PFX.  
       

### <a name="import-a-pfx-certificate"></a>Importación de un certificado PFX

Para importar un certificado PFX, necesitará el SDK de Configuration Manager. Los certificados importados para un usuario se implementarán en todos los dispositivos en que dicho usuario está inscrito.

1. En la página **Certificado PFX** del **Asistente para crear perfil de certificado**, especifique dónde se almacenará el certificado en los dispositivos en que lo va a implementar:
    -     **Instalar en Módulo de plataforma segura (TPM) si está presente**  
    -   **Instalar en Módulo de plataforma segura (TPM) o se producirá un error** 
    -   **Instalar en Windows Hello para empresas o generar un error** 
    -   **Instalar en Proveedor de almacenamiento de claves de software** 
2. Haga clic en **Siguiente**. 
3. En la página **Plataforma admitida** del asistente, seleccione las plataformas de dispositivo en que se instalará este certificado y luego haga clic en **Siguiente**.
4. Use el SDK para Windows 8.1 disponible en el centro de descarga ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)para implementar un script de creación de PFX. El script de creación de PFX agregado en Configuration Manager 2012 SP2 agrega una clase SMS_ClientPfxCertificate al SDK. Esta clase incluye los métodos siguientes:  

    -   ImportForUser  

    -   DeleteForUser  

     Script de ejemplo:  

```  
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

Debe modificar las variables de script siguientes para su script:  

   -   blob\ = blob cifrado en base 64 de PFX  
   -   $Password = contraseña del archivo PFX  
   -   $ProfileName = nombre del perfil PFX  
   -   ComputerName = nombre del equipo host   



### <a name="finish-up"></a>Finalizar

1.  Haga clic en **Siguiente**, revise la página **Resumen** y cierre el asistente.  
2.  El perfil de certificado que contiene el archivo PFX ya está disponible en el área de trabajo **Perfiles de certificado** . 
3.  Para implementar el perfil, en el área de trabajo **Activos y compatibilidad**, abra **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de certificado**, haga clic con el botón derecho en el certificado deseado y luego haga clic en **Implementar**. 



## <a name="see-also"></a>Consulte también
[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) le guiará a través del Asistente para crear perfil de certificado.

[Implementar perfiles de VPN en System Center Configuration Manager de Wi-Fi, VPN, correo electrónico y perfiles de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) proporciona información sobre la implementación de perfiles de certificado.
