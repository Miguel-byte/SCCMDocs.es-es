---
title: "Preparar dispositivos de Windows 10 para la administración conjunta"
description: "Aprenda a preparar dispositivos Windows 10 para la administración conjunta."
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 902787f173c714fd2a73cc657aad758bd79ce3c8
ms.sourcegitcommit: 389c4e5b4e9953b74c13b1689195f99c526fa737
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos de Windows 10 para la administración conjunta
Puede habilitar la administración conjunta en los dispositivos de Windows 10 que están unidos a AD y a Azure AD y que están inscritos en Intune y en un cliente en Configuration Manager. Para los nuevos dispositivos de Windows 10 y para los que ya estén inscritos en Intune, instale el cliente de Configuration Manager antes de administrarlos de forma conjunta. Para los dispositivos de Windows 10 que ya son clientes de Configuration Manager, puede inscribirlos en Intune y habilitar la administración conjunta en la consola de Configuration Manager.

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.

## <a name="command-line-to-install-configuration-manager-client"></a>Línea de comandos para instalar el cliente de Configuration Manager
Debe crear una aplicación en Intune para los dispositivos de Windows 10 que aún no son clientes de Configuration Manager. Al crear la aplicación en las secciones siguientes, use la siguiente línea de comandos:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway*&#62;/ CCMHOSTNAME=&#60;*Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway*&#62; SMSSiteCode=&#60;*CódigoSitio*&#62; SMSMP=https:&#47;/&#60;*FQDN del MP*&#62; AADTENANTID=&#60;*Id. de inquilino de AAD*&#62; AADTENANTNAME=&#60;*Nombre del inquilino*&#62; AADCLIENTAPPID=&#60;*Id. de aplicación del servidor de integración de AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*Id. de recurso*&#62;”

Por ejemplo, si tuviera los siguientes valores:

- **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Use el valor **MutualAuthPath** en la vista SQL **vProxy_Roles** para el valor **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**.

- **FQDN del punto de administración (MP)**: sccmmp.corp.contoso.com    
- **CódigoSitio**: PS1    
- **Id. de inquilino de Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nombre del inquilino de Azure AD**: contoso    
- **Id. de aplicación cliente de Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI del Id. de recurso de AAD**: ConfigMgrServer    

  > [!Note]    
  > Use el valor **IdentifierUri** que se encuentra en la vista SQL **vSMS_AAD_Application_Ex** para el valor **URI del Id. de recurso de AAD**.

Usaría la siguiente línea de comandos:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
> Encontrará los parámetros de la línea de comandos del sitio siguiendo estos pasos:     
> 1. En la consola de Configuration Manager, vaya a **Administración** > **Información general** > **Servicios de nube** > **Co-management** (Administración conjunta).  
> 2. En la pestaña Home (Inicio), en el grupo Manage (Administrar), elija  **Configure co-management** (Configurar administración conjunta) para abrir el Co-management Onboarding Wizard (Asistente para la incorporación de la administración conjunta).    
> 3. En la página de suscripción, haga clic en **Iniciar sesión**, inicie sesión con su inquilino de Intune y haga clic en **Siguiente**.    
> 4. En la página de habilitación, haga clic en **Copiar** en la sección **Devices enrolled in Intune** (Dispositivos inscritos en Intune) para copiar la línea de comandos en el Portapapeles y, luego, guarde la línea de comandos para usarla en el procedimiento en el que se creará la aplicación.  
> 5. Haga clic en **Cancelar** para salir del asistente.

> [!Important]    
> Si personaliza la línea de comandos para instalar el cliente de Configuration Manager, asegúrese de que no supere los 1024 caracteres. Cuando la línea de comandos es mayor de 1024 caracteres, se produce un error en la instalación del cliente.


## <a name="new-windows-10-devices"></a>Nuevos dispositivos de Windows 10
Para los nuevos dispositivos de Windows 10, puede usar el servicio AutoPilot para definir la configuración rápida (OOBE), que incluye la unión del dispositivo a AD y a Azure AD, así como la inscripción del dispositivo en Intune. Luego, cree una aplicación en Intune para implementar el cliente de Configuration Manager.  
1. Habilite AutoPilot para los nuevos dispositivos de Windows 10. Para más información, vea [Resumen de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configure la inscripción automática en Azure AD para que los dispositivos se inscriban automáticamente en Intune. Para más información, vea  [Inscripción de dispositivos Windows para Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Cree una aplicación en Intune con el paquete del cliente de Configuration Manager e implemente la aplicación en los dispositivos de Windows 10 que quiera administrar de forma conjunta. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos necesarios para [instalar los clientes desde Internet mediante Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivos de Windows 10 no inscritos en Intune o en un cliente de Configuration Manager
Para los dispositivos de Windows 10 que no están inscritos en Intune o que tienen el cliente de Configuration Manager, puede usar la inscripción automática para inscribirlos en Intune. Luego, cree una aplicación en Intune para implementar el cliente de Configuration Manager.
1. Configure la inscripción automática en Azure AD para que los dispositivos se inscriban automáticamente en Intune. Para más información, vea  [Inscripción de dispositivos Windows para Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Cree una aplicación en Intune con el paquete del cliente de Configuration Manager e implemente la aplicación en los dispositivos de Windows 10 que quiera administrar de forma conjunta. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos necesarios para [instalar los clientes desde Internet mediante Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivos de Windows 10 inscritos en Intune
Para los dispositivos de Windows 10 que ya están inscritos en Intune, cree una aplicación en Intune para implementar el cliente de Configuration Manager. Use la [línea de comandos para instalar el cliente de Configuration Manager](#command-line-to-install-configuration-manager-client) cuando siga los pasos necesarios para [instalar los clientes desde Internet mediante Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## <a name="next-steps"></a>Pasos siguientes
[Cambio de las cargas de trabajo de Configuration Manager a Intune](co-management-switch-workloads.md)