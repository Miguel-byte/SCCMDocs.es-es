---
title: Administrar los dispositivos basados en internet de forma conjunta
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo preparar los dispositivos basados en internet de Windows 10 para la administración conjunta.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31779b3588617816df4309461ed7715b20b0abd4
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558038"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Cómo preparar los dispositivos basados en internet para la administración conjunta

En este artículo se centra en la segunda ruta de acceso a la administración conjunta, para los nuevos dispositivos basados en internet. Este escenario es cuando haya nuevos dispositivos Windows 10 que unirse a Azure AD e inscribirán automáticamente a Intune. Instalar el cliente de Configuration Manager para llegar a un estado de administración conjunta.  



## <a name="windows-autopilot"></a>Windows Autopilot

Para los nuevos dispositivos Windows 10, puede usar el servicio Autopilot para configurar la configuración rápida (OOBE). Este proceso incluye la unión del dispositivo a Azure AD y será preciso inscribir el dispositivo en Intune.  

Para obtener más información, consulte [información general de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Para configurar los dispositivos se inscriban automáticamente en Intune cuando se unen a Azure AD, consulte [dispositivos de inscripción de Windows para Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Recopilar información de Configuration Manager

A partir de la versión 1802, use Configuration Manager para recopilar y notificar la información del dispositivo requerida por Microsoft Store para Empresas y Educación. Esta información incluye el número de serie del dispositivo, el identificador de producto de Windows y un identificador de hardware. Sirve para registrar el dispositivo en la Microsoft Store para admitir Windows Autopilot. 

1. En la consola de Configuration Manager, vaya a la **supervisión** área de trabajo, expanda el **informes** nodo, expanda **informes**y seleccione el **Hardware: General** nodo.  

2. Ejecute el informe, **información del dispositivo Windows Autopilot**y ver los resultados.  

3. En el Visor de informes, seleccione el **exportar** icono y elija el **CSV (delimitado por comas)** opción.  

4. Después de guardar el archivo, cargue los datos en Microsoft Store para Empresas y Educación.  

Para obtener más información, consulte [agregar dispositivos de Microsoft Store para empresas y educación](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>AutoPilot para los dispositivos existentes
<!--1358333-->

[Windows Autopilot para los dispositivos existentes](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) está disponible en Windows 10, versión 1809 o posterior. Esta característica le permite crear una nueva imagen y aprovisionamiento de un dispositivo de Windows 7 para [modo controlado por el usuario de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) mediante una secuencia de tareas de Configuration Manager única y nativo. 

Para obtener más información, consulte [Windows Autopilot para la secuencia de tareas de dispositivos existente](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).



## <a name="install-the-configuration-manager-client"></a>Instalar al cliente de Configuration Manager

Para dispositivos basados en internet en la segunda ruta de acceso, deberá crear una aplicación en Intune. Implementar esta aplicación en dispositivos Windows 10 que ya no los clientes de Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obtener la línea de comandos de Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  

2. Seleccione el objeto de administración conjunta y, a continuación, elija **propiedades** en la cinta de opciones.  

3. En el **habilitación** pestaña, copie la línea de comandos. Péguelo en el Bloc de notas para guardar para el proceso siguiente.  

La siguiente línea de comandos es un ejemplo: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> A partir de la versión 1806, se necesitan menos propiedades de línea de comandos.  

- Las siguientes propiedades de línea de comandos son necesarias en todos los escenarios:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Las propiedades siguientes son necesarias al usar Azure AD para la autenticación de cliente en lugar de certificados de autenticación de cliente basada en PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Si el cliente se desplaza a la intranet, se requiere la siguiente propiedad:  
    - SMSMP  

- Si no está usando su propio certificado SSL de PKI y la CRL publicada a internet, se requiere el parámetro siguiente:  
    - /noCRLCheck  
    
     Para obtener más información, consulte [planeación para las CRL](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

A partir de la versión 1810, el sitio publica adicionales de Azure información de AD para cloud management gateway (CMG). Un cliente unido a Azure AD obtiene esta información de la instancia de CMG durante el proceso de ccmsetup, mediante el mismo inquilino al que está unido. Este comportamiento simplifica más la inscripción de dispositivos en la administración conjunta de un entorno con más de un inquilino de Azure AD. Ahora son las dos únicas propiedades de ccmsetup necesarias **CCMHOSTNAME** y **SMSSiteCode**.<!--3607731-->

> [!Note]
> Si ya va a implementar al cliente de Configuration Manager en Intune, actualice la aplicación de Intune con una nueva línea de comandos y el nuevo MSI. <!-- SCCMDocs-pr issue 3084 -->

En el ejemplo siguiente se incluye todas estas propiedades:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Crear la aplicación en Intune

1. Vaya a la [portal Azure](https://portal.azure.com)y, a continuación, abra la página de Intune.  

2. Seleccione **las aplicaciones cliente** > **aplicaciones** > **agregar**.  

3. En **Otros**, seleccione **Aplicación de línea de negocio**.  

4. Cargar el **ccmsetup.msi** archivo de paquete de aplicación. Este archivo se encuentra en la siguiente carpeta en el Administrador de configuración del servidor de sitio: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Cuando se actualiza el sitio, asegúrese de que actualizar también esta aplicación en Intune.  

5. Después de la aplicación se actualiza, configure la información de la aplicación con la línea de comandos que ha copiado de Configuration Manager.  

> [!IMPORTANT]    
> Si personaliza esta línea de comandos, asegúrese de que no más de 1024 caracteres. Cuando la longitud de línea de comandos es mayor de 1024 caracteres, se produce un error en la instalación del cliente.


