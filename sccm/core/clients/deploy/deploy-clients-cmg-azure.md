---
title: Instalar el cliente con Azure AD
titleSuffix: Configuration Manager
description: Instale y asigne el cliente de Configuration Manager en dispositivos Windows 10 con Azure Active Directory para la autenticación
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 490e5a614a98633629df98abcd554b02cec1261a
ms.sourcegitcommit: ae03ad403b1732a5a61dec981e3a3010a0f09188
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2018
ms.locfileid: "51860253"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Instalación y asignación de clientes Windows 10 para Configuration Manager mediante la autenticación basada en Azure AD

Para instalar el cliente de Configuration Manager en dispositivos Windows 10 mediante la autenticación de Azure AD, integre Configuration Manager con Azure Active Directory (Azure AD). Los clientes pueden estar en la intranet y comunicarse directamente con un punto de administración habilitado para HTTPS. También pueden basados en Internet y comunicarse a través de CMG o con un punto de administración basado en Internet. Este proceso usa Azure AD para autenticar los clientes en el sitio de Configuration Manager. Azure AD reemplaza la necesidad de configurar y usar certificados de autenticación del cliente.



## <a name="before-you-begin"></a>Antes de comenzar

- Es imprescindible contar con un inquilino de Azure AD.  

- Requisitos del dispositivo:  

    - Windows 10  

    - Estar unido a Azure AD, tanto unido a un dominio en la nube pura como unido a Azure AD híbrido  

- Requisitos del usuario:  

    - El usuario que ha iniciado sesión debe ser una identidad de Azure AD.   

    - Si el usuario es una identidad federada o sincronizada, debe usar la [detección de usuarios de Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) de Configuration Manager, así como la [detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Para obtener más información sobre las identidades híbridas, vea [Definición de una estrategia de adopción de identidad híbrida](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Además de los [requisitos previos existentes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) para el rol de sistema de sitio del punto de administración, habilite también **ASP.NET 4.5** en este servidor. Incluya las demás opciones que se seleccionen automáticamente al habilitar ASP.NET 4.5.  

- Determine si su punto de administración necesita HTTPS. Para obtener más información, vea [Enable management point for HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps) (Habilitar el punto de administración para HTTPS).  

- Opcionalmente, configure una instancia de [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG) para implementar clientes basados en Internet. Para los clientes locales que se autentican con Azure AD, no necesita CMG.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurar Azure Services para la administración en la nube

Como primer paso, conecte el sitio de Configuration Manager a Azure AD. Para obtener detalles de este proceso, vea [Configuración de servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Cree una conexión al servicio de **administración en la nube**.

Habilite la [detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) como parte de la incorporación a la **administración en la nube**. 

Cuando termine estas acciones, el sitio de Configuration Manager estará conectado con Azure AD. 



## <a name="configure-client-settings"></a>Configuración del cliente

Estas opciones de cliente ayudan a unir dispositivos de Windows 10 con Azure AD. También permiten que los clientes basados en Internet usen CMG y el punto de distribución en la nube.

1.  Establezca la siguiente configuración de cliente en la sección **Cloud Services** con la información de [Cómo configurar el cliente](/sccm/core/clients/deploy/configure-client-settings).  

    - **Permitir acceso al punto de distribución en la nube**: habilite esta opción para ayudar a los dispositivos basados en Internet a obtener el contenido requerido para instalar el cliente de Configuration Manager. Si el contenido no está disponible en el punto de distribución en la nube, los dispositivos pueden recuperar el contenido de CMG. El arranque de instalación de cliente reintenta el punto de distribución en la nube durante cuatro horas antes de recurrir a CMG.<!--495533-->  

    - **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory**: establézcalo en **Sí** o **No**. El valor predeterminado es **Sí**. Este comportamiento también es el valor predeterminado de Windows 10, versión 1709.

    - **Permite que los clientes usen una puerta de enlace de administración en la nube**: establézcalo en **Sí** (valor predeterminado) o **No**.  

2.  Implemente la configuración del cliente en la recopilación de dispositivo requerida. No implemente esta configuración en las recopilaciones de usuarios.

Para confirmar que el dispositivo está unido a Azure AD, ejecute `dsregcmd.exe /status` en un símbolo del sistema. El campo **AzureAdjoined** de los resultados mostrará el valor **YES** si el dispositivo se ha unido a Azure AD.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Instalar y registrar el cliente con la identidad de Azure AD

Para instalar manualmente el cliente con la identidad de Azure AD, primero revise el proceso general en [Cómo instalar clientes manualmente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > El dispositivo necesita tener acceso a Internet para ponerse en contacto con Azure AD, pero no hace falta que esté basado en Internet. 

En el ejemplo siguiente se muestra la estructura general de la línea de comandos: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`.

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](/sccm/core/clients/deploy/about-client-installation-properties).

Las propiedades /mp y CCMHOSTNAME especifican uno de los valores siguientes, en función del escenario:
- El punto de administración local. Especifique solo la propiedad /mp. CCMHOSTNAME no es necesario.
- Puerta de enlace de administración en la nube
- El punto de administración basado en Internet. La propiedad SMSMP el especifica el punto de administración local o basado en Internet.

En este ejemplo se usa una instancia de Cloud Management Gateway. Sustituye los valores de ejemplo para cada propiedad: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`.

Para automatizar la instalación del cliente mediante la identidad de Azure AD a través de Microsoft Intune, vea el proceso para [Preparar dispositivos de Windows 10 para la administración conjunta](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Pasos siguientes

Cuando termine, puede seguir [supervisando y administrando clientes](/sccm/core/clients/manage/monitor-clients).
