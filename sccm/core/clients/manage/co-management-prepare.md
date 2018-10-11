---
title: Preparar Windows 10 para la administración conjunta
titleSuffix: Configuration Manager
description: Aprenda a preparar dispositivos Windows 10 para la administración conjunta.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d15484ef38264a5c954dc664f9885b800a078ca6
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601014"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparar dispositivos de Windows 10 para la administración conjunta
Puede habilitar la administración conjunta en los dispositivos de Windows 10 que están unidos a AD y a Azure AD y que están inscritos en Microsoft Intune y en un cliente en Configuration Manager. Para los nuevos dispositivos de Windows 10 y para los que ya estén inscritos en Intune, instale el cliente de Configuration Manager antes de administrarlos de forma conjunta. Para los dispositivos de Windows 10 que ya son clientes de Configuration Manager, puede inscribirlos en Intune y habilitar la administración conjunta en la consola de Configuration Manager.

> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.



## <a name="prerequisites"></a>Requisitos previos

Debe cumplir los siguientes requisitos previos para poder habilitar la administración conjunta. Hay requisitos previos generales y distintos requisitos previos para los dispositivos con el cliente de Configuration Manager y aquellos que no tienen instalado el cliente.


### <a name="general-prerequisites"></a>Requisitos previos generales

A continuación se indican los requisitos previos generales para poder habilitar la administración conjunta:  

- Versión 1710 de Configuration Manager o posterior  

    - A partir de la versión 1806 de Configuration Manager, puede conectar varias instancias de Configuration Manager a un único inquilino de Intune. <!--1357944-->  

- [Sitio incorporado con Azure AD para administración en la nube](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- Licencia de EMS o de Intune para todos los usuarios  

- [Inscripción automática con Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) habilitada  

- Suscripción a Intune y entidad de MDM en Intune establecida en **Intune**.  

    - Si usa una [entidad mixta](/sccm/mdm/deploy-use/migrate-mixed-authority), primero lleve a cabo la migración independiente a Intune. Después, establezca la entidad de MDM a Intune antes de configurar la administración conjunta.<!--SCCMDocs issue #797-->


> [!Note]  
> Si tiene un entorno de MDM híbrido (Intune integrado con Configuration Manager), no puede habilitar la administración conjunta. Sin embargo, puede iniciar la migración de los usuarios a Intune independiente y, después, habilitar sus dispositivos Windows 10 asociados para la administración conjunta. Si quiere saber más sobre la migración a Intune independiente, vea [Iniciar la migración de MDM híbrida a Intune independiente](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### <a name="prerequisite-azure-resource-manager-roles"></a>Requisitos previos de roles de Azure Resource Manager
<!--SCCMDocs issue #667-->Para obtener más información sobre los roles de Azure, vea [Entender los distintos roles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).
|Acción|Rol necesario|
|----|----|
|Configurar una instancia de Cloud Management Gateway|Administrador de suscripción de Azure|
|Configurar un punto de distribución basado en la nube|Administrador de suscripción de Azure|
|Crear aplicaciones de Azure Active Directory desde la consola de Configuration Manager|Administrador global de Azure Active Directory|
|Importar aplicaciones de cliente y servidor de Azure en la consola de Configuration Manager| Administrador de Configuration Manager, no se necesitan roles de Azure adicionales.|
|Configurar la administración conjunta mediante el Asistente para la administración conjunta| Derechos de usuario de Azure Active Directory, junto con ser administrador de Configuration Manager con todos los derechos de ámbito. 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos con el cliente de Configuration Manager

- Windows 10, versión 1709 o posteriores  

- [Unidos a Azure AD híbrido](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (unidos a AD y a Azure AD).  


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Requisitos previos adicionales para los dispositivos sin el cliente de Configuration Manager

- Windows 10, versión 1709 o posteriores  

- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) en Configuration Manager (al usar Intune para instalar el cliente de Configuration Manager)  


> [!IMPORTANT]
> Los dispositivos móviles con Windows 10 no admiten la administración conjunta.



## <a name="command-line-to-install-configuration-manager-client"></a>Línea de comandos para instalar el cliente de Configuration Manager

Cree una aplicación en Intune para los dispositivos de Windows 10 que aún no son clientes de Configuration Manager. Al crear la aplicación en las secciones siguientes, use la siguiente línea de comandos:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line"></a>Ejemplo de línea de comandos
Si tiene los siguientes valores:

- **URL del extremo de autenticación mutua de la puerta de enlace de administración en la nube**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!Note]    
   >Use el valor **MutualAuthPath** en la vista SQL **vProxy_Roles** para el valor **Dirección URL del punto de conexión de autenticación mutua de Cloud Management Gateway**.  

- **FQDN de punto de administración (MP)**: `mp1.contoso.com`    
- **CódigoSitio**: `PS1`    
- **Id. de inquilino de Azure AD**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **Id. de aplicación de cliente de Azure AD**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **URI de id. de recurso de AAD**: `ConfigMgrServer`    

  > [!Note]    
  > Use el valor **IdentifierUri** que se encuentra en la vista SQL **vSMS_AAD_Application_Ex** para el valor **URI del Id. de recurso de AAD**.  

Después use la siguiente línea de comandos:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> A partir de la versión 1806, se necesitan menos propiedades de línea de comandos.  

- Las siguientes propiedades de línea de comandos son necesarias en todos los escenarios:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Las propiedades siguientes son necesarias al usar Azure AD para la autenticación de cliente en lugar de certificados de autenticación de cliente basada en PKI:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- La siguiente propiedad es obligatoria si el cliente volverá a la intranet:  
    - SMSMP  

En el ejemplo siguiente se incluyen todas las propiedades anteriores:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Para obtener más información, vea [Acerca de las propiedades de instalación de clientes](/sccm/core/clients/deploy/about-client-installation-properties).


> [!Tip]
> Encontrará los parámetros de la línea de comandos del sitio siguiendo estos pasos:     
> 
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**.  
> 
> 2. En la cinta, seleccione **Configurar administración conjunta** para abrir el Asistente para incorporación de la administración conjunta. Si ya configuró la administración conjunta, seleccione **Propiedades**. Después, vaya al paso 4.    
> 
> 3. En la página de suscripción, seleccione **Iniciar sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.    
> 
> 4. En la página de habilitación, seleccione **Copiar** para copiar la línea de comandos en el Portapapeles. Después guarde la línea de comandos que va a usar en el procedimiento para crear la aplicación.  
> 
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
