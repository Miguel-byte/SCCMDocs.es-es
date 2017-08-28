---
title: "Instalación y asignación del cliente desde Internet | Microsoft Docs"
description: Instale y asigne al cliente de System Center Configuration Manager desde Internet.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: es-es
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>Instalación y asignación de clientes de Configuration Manager desde Internet mediante Azure AD con fines de autenticación

Puede usar los servicios en la nube de Configuration Manager con Azure AD para admitir los escenarios siguientes:

- Instalación manual del cliente de Configuration Manager desde Internet y asignación a un sitio de Configuration Manager (requiere el rol de sistema de sitio de Cloud Management Gateway).
- Uso de Azure AD para autenticar los clientes en Internet para acceder a los sitios de Configuration Manager. Azure AD reemplaza la necesidad de configurar y usar certificados de autenticación del cliente.
- Puede detectar usuarios de Azure AD en el sitio para usarlos en las recopilaciones y otras operaciones de Configuration Manager.

Use los siguientes temas siguientes para ayudarlo a realizar esta tarea:

- **Paso 1: Configuración de Cloud Management Gateway**
- **Paso 2: Configuración de la aplicación de servicios de Azure en Configuration Manager Cloud Services**
- **Paso 3: Configuración del cliente para registrar dispositivos Windows 10 con Azure AD**
- **Paso 4: Instalación y registro del cliente de Configuration Manager con Azure Active Directory Identity Protection**


## <a name="before-you-start"></a>Antes de empezar

- Debe tener un inquilino de Azure AD.
- Los dispositivos deben ejecutar Windows 10 y estar unidos a Azure AD. (Además de a Azure AD, los clientes también pueden estar unidos a un dominio).
- Además de los [requisitos previos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) para el rol de sistema de sitio del punto de administración, debe asegurarse de que la plataforma **ASP.NET 4.5** (y cualquier otra opción que se seleccione automáticamente) esté habilitada en el equipo que hospeda este rol de sistema de sitio.
- Para usar Configuration Manager para implementar el cliente:
    - Configure al menos un punto de administración para el modo HTTPS.
    - Configure una instancia de Cloud Management Gateway.

## <a name="step-1-set-up-the-cloud-management-gateway"></a>Paso 1: Configuración de Cloud Management Gateway

Configure Cloud Management Gateway para permitir que los clientes accedan a su sitio de Configuration Manager en Internet sin utilizar certificados. Busque ayuda en los temas siguientes: 

- [Planificación de Cloud Management Gateway en Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway)
- [Configurar puerta de enlace de administración en la nube para Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway)
- [Supervisar la puerta de enlace de administración en la nube en Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway)

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Paso 2: Configuración de la aplicación de servicios de Azure en Configuration Manager Cloud Services

Con esta acción se conecta el sitio de Configuration Manager con Azure AD, lo cual es un requisito previo para todas las demás operaciones de esta sección. 

La funcionalidad de detección de usuarios de Azure AD está configurada como parte de *Cloud Management Gateway*. El procedimiento se detalla en el paso **6** de la sección [Creación de la aplicación web de Azure para utilizarla Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) del tema *Configuración de servicios de Azure para utilizarlos con Configuration Manager*.
    
Cuando termine el procedimiento, ya habrá conectado el sitio de Configuration Manager con Azure AD. 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>Paso 3: Configuración del cliente para registrar dispositivos Windows 10 con Azure AD

1.  Establezca la siguiente sección de configuración de cliente (que se encuentra en Cloud Services) con la información de [Cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).
    - **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory**: establézcalo en **Sí** (valor predeterminado) o **No**.
    - **Permite que los clientes usen una puerta de enlace de administración en la nube**: establézcalo en **Sí** (valor predeterminado) o **No**.
2.  Implemente la configuración del cliente en la recopilación de dispositivo requerida.

Para confirmar que el dispositivo está unido a Azure AD, ejecute el comando **dsregcmd.exe /status** en una ventana del símbolo del sistema. El campo **AzureAdjoined** de los resultados mostrará el valor **YES** si el dispositivo se ha unido a Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Paso 4: Instalación y registro del cliente de Configuration Manager con Azure Active Directory Identity Protection

Antes de empezar, asegúrese de que los archivos de origen de la instalación del cliente están almacenados localmente en el dispositivo en el que desea instalar el cliente. Después, siga las instrucciones de [Implementación de clientes en equipos Windows con System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) mediante la siguiente línea de comandos de instalación: 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**: si el punto de administración o la instancia de Cloud Management Gateway usa un certificado de servidor no público, es posible que el cliente no pueda acceder a la ubicación de CRL.
- **/Source**: carpeta local; la ubicación de los archivos de instalación del cliente.
- **CCMHOSTNAME**: nombre del punto de administración de Internet. Puede encontrarlo mediante la ejecución de **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** desde un símbolo del sistema en un cliente administrado.
- **SMSMP**: nombre del punto de administración de búsqueda (puede ser de la intranet).
- **SMSSiteCode**: código de sitio del sitio de Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: identificador y nombre del inquilino de Azure AD vinculados a Configuration Manager. Puede encontrarlos mediante la ejecución de dsregcmd.exe /status desde un símbolo del sistema en un dispositivo unido a Azure AD.
- **AADCLIENTAPPID**: identificador de la aplicación cliente de Azure AD. Para encontrarlo, consulte [Uso del portal para crear una aplicación de Azure Active Directory y una entidad de servicio con acceso a los recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: identificador URI de la aplicación de servidor de Azure AD incorporada.


## <a name="next-steps"></a>Pasos siguientes

Cuando termine, puede seguir [supervisando y administrando clientes](/sccm/core/clients/manage/monitor-clients).
