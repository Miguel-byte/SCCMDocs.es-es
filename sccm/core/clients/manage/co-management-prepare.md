---
title: Preparar Windows 10 para la administración conjunta
titleSuffix: Configuration Manager
description: Aprenda a preparar dispositivos Windows 10 para la administración conjunta.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: 93a991cb3fd78e44f5ae4434a9845a57450e1025
ms.sourcegitcommit: e4ca9fb1fad2caaf61bb46e0a12f4d6b96f15513
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos de Windows 10 para la administración conjunta
Puede habilitar la administración conjunta en los dispositivos de Windows 10 que están unidos a AD y a Azure AD y que están inscritos en Microsoft Intune y en un cliente en Configuration Manager. Para los nuevos dispositivos de Windows 10 y para los que ya estén inscritos en Intune, instale el cliente de Configuration Manager antes de administrarlos de forma conjunta. Para los dispositivos de Windows 10 que ya son clientes de Configuration Manager, puede inscribirlos en Intune y habilitar la administración conjunta en la consola de Configuration Manager.

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.


## <a name="prerequisites"></a>Requisitos previos
Debe cumplir los siguientes requisitos previos para poder habilitar la administración conjunta. Hay requisitos previos generales y distintos requisitos previos para los clientes con el cliente de Configuration Manager y los dispositivos que no tienen instalado el cliente.
### <a name="general-prerequisites"></a>Requisitos previos generales
A continuación se indican los requisitos previos generales para poder habilitar la administración conjunta:  

- Versión 1710 de Configuration Manager o posterior
- Azure AD
- Licencia de EMS o de Intune para todos los usuarios
- [Inscripción automática con Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitada
- Suscripción a Intune &#40;entidad de MDM en Intune establecida en **Intune**&#41;


   > [!Note]  
   > Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos con el cliente de Configuration Manager
- Windows 10, versión 1709 o posteriores
- [Unidos a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (unidos a AD y a Azure AD)

### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos sin el cliente de Configuration Manager
- Windows 10, versión 1709 o posteriores
- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) en Configuration Manager (al usar Intune para instalar el cliente de Configuration Manager)

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.


## <a name="command-line-to-install-configuration-manager-client"></a>Línea de comandos para instalar el cliente de Configuration Manager
Cree una aplicación en Intune para los dispositivos de Windows 10 que aún no son clientes de Configuration Manager. Al crear la aplicación en las secciones siguientes, use la siguiente línea de comandos:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

Por ejemplo, si tuviera los siguientes valores:

- **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    

   >[!Note]    
   >Use el valor **MutualAuthPath** en la vista SQL **vProxy_Roles** para el valor **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**.

- **FQDN del punto de administración (MP)**: mp1.contoso.com    
- **CódigoSitio**: PS1    
- **Identificador de inquilino de Azure AD**: 60a413f4 c606 4744 8adb 9476ae3XXXXX    
- **Identificador de aplicación cliente de Azure AD**: 9fb9315f-4c42-405f-8664-ae63283XXXXX     
- **URI del Id. de recurso de AAD**: ConfigMgrServer    

  > [!Note]    
  > Use el valor **IdentifierUri** que se encuentra en la vista SQL **vSMS_AAD_Application_Ex** para el valor **URI del Id. de recurso de AAD**.

Usaría la siguiente línea de comandos:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=60a413f4-c606-4744-8adb-9476ae3XXXXX AADCLIENTAPPID=9fb9315f-4c42-405f-8664-ae63283XXXXX AADRESOURCEURI=https://ConfigMgrServer"`

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

   > [!NOTE]   
   > A partir de la versión 1802, use Configuration Manager para recopilar y notificar la información del dispositivo requerida por Microsoft Store para Empresas y Educación. Esta información incluye el número de serie del dispositivo, el identificador de producto de Windows y un identificador de hardware. En la consola de Configuration Manager, área de trabajo **Supervisión**, expanda el nodo **Generación de informes**, expanda **Informes** y seleccione el nodo **Hardware - General**. Ejecute el nuevo informe con **información de dispositivo Windows AutoPilot** y observe los resultados. En el visor de informes, haga clic en el icono **Exportar** y seleccione la opción **CSV (delimitado por comas)**. Después de guardar el archivo, cargue los datos en Microsoft Store para Empresas y Educación. Para obtener más información, consulte [Add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) (Agregar dispositivos en Microsoft Store para Empresas y Educación).

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