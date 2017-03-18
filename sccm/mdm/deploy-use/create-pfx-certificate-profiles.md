---
title: Crear perfiles de certificado PFX | Microsoft Docs
description: "Obtenga información sobre cómo usar archivos PFX en System Center Configuration Manager para generar certificados específicos del usuario que admiten el intercambio de datos cifrados."
ms.custom: na
ms.date: 03/05/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de certificados PFX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Los perfiles de certificado trabajan con los Servicios de certificados de Active Directory y el rol Servicio de inscripción de dispositivos de red para aprovisionar certificados de autenticación para dispositivos administrados para que los usuarios puedan acceder sin problemas a los recursos de empresa. Por ejemplo, puede crear e implementar perfiles de certificado para proporcionar los certificados necesarios para que los usuarios inicien conexiones VPN e inalámbricas.

Los [perfiles de certificado](../../protect/deploy-use/introduction-to-certificate-profiles.md) proporcionan información general sobre la creación y configuración de perfiles de certificado. En este tema se destaca información específica sobre perfiles de certificado relacionados con la administración de dispositivos móviles.

- Los perfiles de certificado proporcionan inscripción y renovación de certificados desde una entidad de certificación (CA) empresarial para dispositivos que ejecutan iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop y Mobile, y Android. Estos certificados se pueden usar en conexiones Wi-Fi y VPN.

-  Para implementar perfiles de certificado que usen SCEP, debe instalar un módulo de directivas para NDES en un servidor que ejecute Windows Server 2012 R2 con el rol Servicios de certificados de Active Directory y un NDES operativo y al que los dispositivos que precisan certificados puedan acceder. Para dispositivos inscritos por Microsoft Intune, se requiere poder tener acceso al NDES desde Internet, por ejemplo, en una subred filtrada (también se conoce como red perimetral).

-  Configuration Manager admite la implementación de certificados en varios almacenes de certificados distintos en función de los requisitos, el tipo de dispositivo y el sistema operativo. Se admiten los dispositivos y los sistemas operativos siguientes:
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop y Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  Para implementar perfiles en dispositivos Android, iOS, Windows Phone y Windows 8.1 o posterior inscritos, estos dispositivos deben [inscribirse en Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

- Para información sobre otros requisitos previos, consulte [Requisitos previos de perfiles de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Perfiles de certificado PFX
System Center Configuration Manager permite aprovisionar archivos de intercambio de información personal (.pfx) en los dispositivos de usuario. Los archivos PFX pueden usarse para generar certificados específicos del usuario para admitir el intercambio de datos cifrados. Los certificados PFX pueden crearse en Configuration Manager o importarse. Con System Center Configuration Manager, los certificados PFX nuevos o importados pueden implementarse en dispositivos iOS, Android y Windows 10. A continuación, estos archivos se pueden implementar en varios dispositivos para admitir la comunicación de PKI basada en usuario.  

> [!TIP]  
>  En [Cómo crear e implementar perfiles de certificado PFX en Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)también encontrará un tutorial detallado en el que se describe este proceso.  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creación e implementación de un perfil de certificado de intercambio de información personal (PFX)  

1.  En la consola de System Center Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , expanda **Configuración de cumplimiento**, expanda **Acceso a los recursos de la compañía**y, a continuación, haga clic en **Perfiles de certificado**.  

3.  En la pestaña **Inicio** del grupo **Crear** , haga clic en **Crear perfil de certificado**. El asistente para **Crear perfil de certificado** se abre.  

4.  En la página **General** del asistente para **Crear perfil de certificado** , especifique la información siguiente:  

    -   **Nombre**: escriba un nombre único para el perfil de certificado. Puede utilizar un máximo de 256 caracteres.  

    -   **Descripción**: facilite una descripción general del perfil de certificado y cualquier otra información adicional pertinente para identificarlo en la consola de System Center Configuration Manager. Puede utilizar un máximo de 256 caracteres.  

    -   **Especifique el tipo de perfil de certificado que desea crear**: elija uno de los tipos de perfil de certificado que se indican a continuación.  

        -   **Certificado de CA de confianza**: seleccione este tipo de perfil de certificado si desea implementar un certificado de entidad de certificación raíz (CA) de confianza o uno intermedio para formar una cadena de certificados de confianza en los casos en los que el usuario o el dispositivo deban autenticar otro dispositivo. Por ejemplo, el dispositivo puede ser un servidor de Servicio de autenticación remota telefónica de usuario (RADIUS) o un servidor de red privada virtual (VPN). También debe configurar un perfil de certificado de CA de confianza antes de crear un perfil de certificado de SCEP. En este caso, el certificado de CA de confianza debe ser el certificado raíz de confianza de la CA que emitirá el certificado para el usuario o el dispositivo.  

        -   **Configuración de Protocolo de inscripción de certificados simple (SCEP)**: seleccione este tipo de perfil de certificado si desea solicitar un certificado para un dispositivo o usuario mediante el Protocolo de inscripción de certificados simple y el servicio de rol Servicio de inscripción de dispositivos de red.  

        -   **Intercambio de información personal: configuración de PKCS #12 (PFX): importar**: seleccione esta opción para importar un certificado PFX.  

5.  En la ventana **Propiedades del certificado** del asistente para **Crear perfil de certificado** , especifique dónde se almacenarán los certificados PFX en los dispositivos de destino.  

    -   **Instalar en Módulo de plataforma segura (TPM) si está presente**  

    -   **Instalar en Módulo de plataforma segura (TPM) o se producirá un error**  

    -   **Instalar en Proveedor de almacenamiento de claves de software**  

     Haga clic en **Siguiente**.  

6.  En la ventana **Plataformas compatibles** del asistente para **Crear perfil de certificado** , especifique qué sistemas operativos o plataformas pueden recibir el archivo PFX importado.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Haga clic en **Siguiente**, revise la página **Resumen** y cierre el asistente.  

8.  El perfil de certificado que contiene el archivo PFX ya está disponible en el área de trabajo **Perfiles de certificado** . En la consola de **Activos y compatibilidad** , vaya a **Configuración de cumplimiento** > **Acceso a los recursos de la compañía** > **Perfiles de certificado** y haga clic con el botón derecho para implementar el nuevo certificado en recopilaciones de usuarios.  

9. Use el SDK para Windows 8.1 disponible en el centro de descarga ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525)para implementar un script de creación de PFX. El script de creación de PFX agregado en Configuration Manager 2012 SP2 agrega una clase SMS_ClientPfxCertificate al SDK. Esta clase incluye los métodos siguientes:  

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

    -   <blob\> = blob cifrado en base&64; de PFX  

    -   $Password = contraseña del archivo PFX  

    -   $ProfileName = nombre del perfil PFX  

    -   ComputerName = nombre del equipo host  

### <a name="see-also"></a>Consulte también
[Crear un nuevo perfil de certificado](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) le guiará a través del Asistente para crear perfil de certificado.

[Implementar perfiles de VPN en System Center Configuration Manager de Wi-Fi, VPN, correo electrónico y perfiles de certificado](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) proporciona información sobre la implementación de perfiles de certificado.

