---
title: Crear perfiles de certificados PFX | System Center Configuration Manager
description: "Obtenga información sobre cómo usar archivos PFX en System Center Configuration Manager para generar certificados específicos del usuario que admiten el intercambio de datos cifrados."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0185ab18-663d-468a-ba54-4f3f232fd4d2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4a4025325e635061cb99caed9cdb07390e90ea90


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Cómo crear perfiles de certificados PFX en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


System Center Configuration Manager permite aprovisionar archivos de intercambio de información personal (.pfx) en los dispositivos de usuario. Los archivos PFX pueden usarse para generar certificados específicos del usuario para admitir el intercambio de datos cifrados. Los certificados PFX pueden crearse en Configuration Manager o importarse. Con System Center Configuration Manager, los certificados PFX nuevos o importados pueden implementarse en dispositivos iOS, Android y Windows 10. A continuación, estos archivos se pueden implementar en varios dispositivos para admitir la comunicación de PKI basada en usuario.  

> [!TIP]  
>  En [Cómo crear e implementar perfiles de certificado PFX en Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)también encontrará un tutorial detallado en el que se describe este proceso.  

## <a name="create-and-deploy-personal-information-exchange-pfx-certificate-profiles"></a>Crear e implementar perfiles de certificado de intercambio de información personal (PFX)  

#### <a name="how-to-create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Cómo crear e implementar un perfil de certificado de intercambio de información personal (PFX)  

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

    -   <blob\> = blob cifrado en base 64 de PFX  

    -   $Password = contraseña del archivo PFX  

    -   $ProfileName = nombre del perfil PFX  

    -   ComputerName = nombre del equipo host  



<!--HONumber=Nov16_HO1-->


