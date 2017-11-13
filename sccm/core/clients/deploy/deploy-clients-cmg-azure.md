---
title: "Instalación y asignación del cliente desde Internet"
titleSuffix: Configuration Manager
description: Instale y asigne al cliente de System Center Configuration Manager desde Internet.
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 2ef7580f94864094e9420eb0f5a5c5b4dc9d6d24
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD

Puede usar los servicios en la nube de Configuration Manager con Azure AD para admitir los escenarios siguientes:

- Instalación manual del cliente de Configuration Manager en dispositivos con Windows 10 desde Internet y asignación a un sitio de Configuration Manager (requiere el rol de sistema de sitio de Cloud Management Gateway).
- Uso de Azure AD para autenticar los clientes para acceder a los sitios de Configuration Manager. Azure AD reemplaza la necesidad de configurar y usar certificados de autenticación del cliente.
- Puede detectar usuarios de Azure AD en el sitio para usarlos en las recopilaciones y otras operaciones de Configuration Manager.

Use los siguientes temas siguientes para ayudarlo a realizar esta tarea:

- **Paso 1: Configuración de la aplicación de servicios de Azure en Configuration Manager Cloud Services y configuración de la detección de usuarios de Azure AD**
- **Paso 2: Configuración de Cloud Management Gateway** (opcional para clientes locales)
- **Paso 3: Configuración de cliente para conectar dispositivos con Windows 10 a Azure AD y habilitar a los clientes para que usen Cloud Management Gateway**
- **Paso 4: Instalación y registro del cliente de Configuration Manager con Azure Active Directory Identity Protection**


## <a name="before-you-start"></a>Antes de empezar

- Debe tener un inquilino de Azure AD.
- Los dispositivos deben ejecutar Windows 10, estar conectados a Azure AD y registrarse con una identidad de Azure AD. (Además de a Azure AD, los clientes también pueden estar unidos a un dominio).
- Además de los [requisitos previos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para el rol de sistema de sitio del punto de administración, debe asegurarse de que la plataforma **ASP.NET 4.5** (y cualquier otra opción que se seleccione automáticamente) esté habilitada en el equipo que hospeda este rol de sistema de sitio.
- Para usar Configuration Manager para implementar el cliente:
    - Configure al menos un punto de administración para el modo HTTPS si desea usar Azure AD para autenticación en lugar de certificados de cliente.
        Si usa certificados de cliente en lugar de Cloud Management Gateway, un punto de administración de HTTPS es opcional, pero recomendable. Si usa Azure AD para autenticación, ya sea para clientes locales o de Internet, se requiere el punto de administración de HTTPS.
    - Configure una instancia de Cloud Management Gateway si desea implementar clientes de Internet. Para los clientes locales, que se autentican con Azure AD, no es necesario configurar Cloud Management Gateway.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Paso 1: Configuración de la aplicación de servicios de Azure en Configuration Manager Cloud Services

Con esta acción se conecta el sitio de Configuration Manager con Azure AD, lo cual es un requisito previo para todas las demás operaciones de esta sección. 

La funcionalidad de detección de usuarios de Azure AD está configurada como parte de *Cloud Management Gateway*. El procedimiento se detalla en el paso **6** de la sección [Creación de la aplicación web de Azure para utilizarla Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) del tema *Configuración de servicios de Azure para utilizarlos con Configuration Manager*.
    
Cuando termine el procedimiento, ya habrá conectado el sitio de Configuration Manager con Azure AD. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Paso 2: Configuración de Cloud Management Gateway

Configure Cloud Management Gateway para ayudar a habilitar los escenarios de administración en la nube descritos en este tema. Busque ayuda en los temas siguientes: 

- [Planificación de Cloud Management Gateway en Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Configurar puerta de enlace de administración en la nube para Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Supervisar la puerta de enlace de administración en la nube en Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Paso 3: Configuración de cliente para conectar dispositivos con Windows 10 a Azure AD y habilitar a los clientes para que usen Cloud Management Gateway

1.  Establezca la siguiente sección de configuración de cliente **que se encuentra en Cloud Services** con la información de [Cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).
    - **Permitir acceso al punto de distribución de nube**: habilite esta opción para ayudar a dispositivos basados en Internet a obtener el contenido requerido para instalar el cliente de Configuration Manager. Si el contenido no está disponible en el punto de distribución de nube, los dispositivos pueden recuperar el contenido desde un punto de administración conectado a Cloud Management Gateway.
    - **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory**: establézcalo en **Sí** (valor predeterminado) o **No**.
    - **Permite que los clientes usen una puerta de enlace de administración en la nube**: establézcalo en **Sí** (valor predeterminado) o **No**.
2.  Implemente la configuración del cliente en la recopilación de dispositivo requerida. No implemente esta configuración en las recopilaciones de usuarios.

Para confirmar que el dispositivo está unido a Azure AD, ejecute el comando **dsregcmd.exe /status** en una ventana del símbolo del sistema. El campo **AzureAdjoined** de los resultados mostrará el valor **YES** si el dispositivo se ha unido a Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Paso 4: Instalación y registro del cliente de Configuration Manager con Azure Active Directory Identity Protection

Para instalar el cliente, siga las instrucciones de [Implementación de clientes en equipos Windows con System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) mediante la siguiente línea de comandos de instalación: 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP**: origen de la descarga. Puede establecerlo en CMG si arranca desde Internet.
- **CCMHOSTNAME**: nombre del punto de administración de Internet. Puede encontrarlo mediante la ejecución de **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** desde un símbolo del sistema en un cliente administrado.
- **SMSSiteCode**: código de sitio del sitio de Configuration Manager.
- **SMSMP**: nombre del punto de administración de búsqueda (puede ser de la intranet).
- **AADTENANTID**, **AADTENANTNAME**: identificador y nombre del inquilino de Azure AD vinculados a Configuration Manager. Puede encontrarlos mediante la ejecución de dsregcmd.exe /status desde un símbolo del sistema en un dispositivo unido a Azure AD.
- **AADCLIENTAPPID**: identificador de la aplicación cliente de Azure AD. Para encontrarlo, consulte [Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: identificador URI de la aplicación de servidor de Azure AD incorporada. Para más información, vea [Configuración de servicios de Azure para utilizarlos con Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Pasos siguientes

Cuando termine, puede seguir [supervisando y administrando clientes](/sccm/core/clients/manage/monitor-clients).
