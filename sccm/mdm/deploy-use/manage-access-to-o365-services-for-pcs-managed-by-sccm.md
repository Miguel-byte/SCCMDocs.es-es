---
title: Administrar el acceso a servicios de Office 365
titleSuffix: Configuration Manager
description: Aprenda a configurar el acceso condicional a los servicios de Office 365 en equipos administrados por System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 434801b170ed5efcbbafa046a3ac1e94a615ed3d
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196779"
---
# <a name="manage-access-to-office-365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Administrar el acceso a servicios de Office 365 para equipos administrados por System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1191496-->
Configure el acceso condicional a los servicios de Office 365 en equipos administrados por Configuration Manager.  

> [!Important]  
> Incluida de MDM híbrida local son de acceso condicional [características en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
> 
> Si usa acceso condicional en los dispositivos administrados con el cliente de Configuration Manager, para asegurarse de que todavía están protegidos, habilitar el acceso condicional en Intune para los dispositivos antes de migrar. Habilitar la administración conjunta en Configuration Manager, mover la carga de trabajo de directiva de cumplimiento a Intune y, a continuación, complete la migración de Intune híbrido a Intune independiente. Para obtener más información, consulte [el acceso condicional con administración conjunta](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 


Para obtener información sobre cómo configurar el acceso condicional para dispositivos inscritos y administrados por Microsoft Intune, vea [Administrar el acceso a servicios en System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). En ese artículo también se describen los dispositivos que están unidos a un dominio y no se evalúan para cumplimiento.

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="supported-services"></a>Servicios compatibles  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>Equipos compatibles  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Servidores de Windows compatibles

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > En el caso de servidores de Windows que puedan tener varios usuarios que hayan iniciado sesión de manera simultánea, implemente las mismas directivas de acceso condicional en todos esos usuarios.

## <a name="configure-conditional-access"></a>Configuración de acceso condicional  
 Para configurar el acceso condicional, primero debe crear una directiva de cumplimiento y configurar la directiva de acceso condicional. Al configurar directivas de acceso condicional para PC, puede requerir que los PC cumplan la directiva para tener acceso a los servicios Exchange Online y SharePoint Online.  

### <a name="prerequisites"></a>Requisitos previos  

- Sincronización de AD FS y una suscripción de Office 365. La suscripción de Office 365 es cómo configurar Exchange Online y SharePoint Online.  

- Suscripción a Microsoft Intune. La suscripción a Microsoft Intune debe configurarse en la consola de Configuration Manager. La suscripción de Intune se utiliza para retransmitir el estado de cumplimiento de los dispositivos a Azure Active Directory y para las licencias de usuario.  

  Los equipos deben cumplir los requisitos siguientes:  

- [Requisitos previos](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) para el registro automático de dispositivos con Azure Active Directory  

   Puede registrar equipos con Azure AD a través de la directiva de cumplimiento.  

  -   Para equipos con Windows 8.1 y Windows 10, puede usar una directiva de grupo de Active Directory para configurar los dispositivos a fin de que se registren automáticamente en Azure AD.  

  -   Para equipos con Windows 7, debe implementar el paquete de software de registro de dispositivo en el equipo con Windows 7 a través de System Center Configuration Manager. Puede encontrar más información en el artículo [Registro automático de dispositivos en Azure Active Directory para dispositivos Windows unidos a un dominio](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).  

- Debe usar Office 2013 u Office 2016 con la autenticación moderna [habilitada](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

  Los pasos siguientes se aplican a Exchange Online y SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Paso 1. Configurar directiva de cumplimiento  
 En la consola de Configuration Manager, cree una directiva de cumplimiento con las reglas siguientes:  

-   **Requerir registro en Azure Active Directory:** Esta regla comprueba si el dispositivo del usuario es el lugar de trabajo unido a Azure AD y, si no, el dispositivo se registra automáticamente en Azure AD. El registro automático solo se admite en Windows 8.1. Para equipos con Windows 7, implemente un archivo MSI para realizar el registro automático. Para más información, vea [Registro automático de dispositivos en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **Todas las actualizaciones necesarias que se instalan con una fecha límite anterior a un número determinado de días:** Especifique el valor para el período de gracia de la fecha límite de implementación para las actualizaciones necesarias en el dispositivo del usuario. Al agregar esta regla también se instalan automáticamente todas las actualizaciones necesarias pendientes. Especifique las actualizaciones necesarias en la regla **Actualizaciones automáticas requeridas**.   

-   **Requerir cifrado de unidad BitLocker:** Esta regla comprueba si la unidad principal (por ejemplo, C:\\) en el dispositivo está cifrada con BitLocker. Si BitLocker no está habilitado el cifrado en el dispositivo primario, el acceso al correo electrónico y SharePoint services está bloqueado.  

-   **Requerir antimalware:** Esta regla comprueba si System Center Endpoint Protection o Windows Defender está habilitado y ejecutándose. Si no está habilitado, se bloquea el acceso a los servicios de correo electrónico y SharePoint.  

-   **Informe del estado correcto por el servicio de atestación de estado:** Esta condición incluye cuatro subreglas para comprobar el cumplimiento del dispositivo en el servicio de atestación de estado de dispositivo. Para más información, vea [Atestación de estado](/sccm/core/servers/manage/health-attestation). 

    - **Debe estar habilitado BitLocker en el dispositivo**
    - **Debe estar habilitado el arranque seguro en el dispositivo** 
    - **Debe estar habilitada la integridad de código en el dispositivo**
    - **Debe estar habilitado el antimalware de inicio temprano en el dispositivo**  

    >[!Tip]  
    > Los criterios de acceso condicional de atestación de estado del dispositivo, que se introdujeron con la versión 1710, son una [característica de versión preliminar](/sccm/core/servers/manage/pre-release-features). A partir de la versión 1802, ya no es una característica de versión preliminar.<!--1235616-->  

    > [!Note]  
    > Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Paso 2. Evaluar el impacto del acceso condicional  
 Ejecute el **informe de compatibilidad de acceso condicional**. Se puede encontrar en el área de trabajo **Supervisión**, en **Informes** > **Administración de compatibilidad y configuración**. En este informe se muestra el estado de cumplimiento para todos los dispositivos. Se bloquea el acceso de los dispositivos registrados como no compatibles a Exchange Online y SharePoint Online.  

 ![Consola de Configuration Manager, área de trabajo supervisión, informes, informes, cumplimiento y administración de configuración: Informe de cumplimiento de acceso condicional](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar grupos de seguridad de Active Directory  
 Las directivas de acceso condicional se dirigen a grupos de usuarios en función de los tipos de directivas. Estos grupos contienen los usuarios destinatarios de la directiva o exentos de ella. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso al servicio.  

 Grupos de usuarios de seguridad de Active Directory Estos grupos de usuarios se deben sincronizar con Azure Active Directory. También puede configurar estos grupos en el centro de administración de Microsoft 365 o el portal de cuentas de Intune.  

 Se pueden especificar dos tipos de grupo en cada directiva. :  

-   **Grupos destinatarios**: grupos de usuarios a los que se aplica la directiva. Debe usarse el mismo grupo para la directiva de cumplimiento y de acceso condicional.  

-   **Grupos exentos**: grupos de usuarios que están exentos de la directiva (opcional).  
    Si un usuario pertenece a ambos, está exento de la directiva.  

     Solo se evalúan los grupos que son destinatarios de la directiva de acceso condicional.  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Paso 3. Crear una directiva de acceso condicional para Exchange Online y SharePoint Online  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  Para crear una directiva para Exchange Online, seleccione **Habilitar directiva de acceso condicional para Exchange Online**.  

     Para crear una directiva para SharePoint Online, seleccione **Habilitar directiva de acceso condicional para Exchange Online**.  

3.  En la pestaña **Inicio** , en el grupo **Vínculos** , haga clic en **Configurar directiva de acceso condicional en la consola de Intune**. Puede que deba proporcionar el nombre de usuario y la contraseña de la cuenta utilizada para conectar Configuration Manager con Intune.  

     Se abre la consola de administración de Intune.  

4.  Para Exchange Online, en la consola de administración de Microsoft Intune, haga clic en **Directiva > Acceso condicional > Directiva de Exchange Online**.  

     Para SharePoint Online, en la consola de administración de Microsoft Intune, haga clic en **Directiva > Acceso condicional > Directiva de SharePoint Online**.  

5.  Defina el requisito de equipos Windows con la opción**Los dispositivos deben ser compatibles**.  

6.  En **Grupos destinatarios**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplica la directiva.  

    > [!NOTE]  
    >  Debe usarse el mismo grupo de usuarios de seguridad para implementar la directiva de cumplimiento y el grupo de destino de la directiva de acceso condicional.  

     En **Grupos exentos**, opcionalmente, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory que se van a excluir de la directiva.  

7.  Haga clic en **Guardar** para crear y guardar la directiva.  

Los usuarios ven la información de cumplimiento en el Centro de software. Cuando se bloqueen debido al no cumplimiento, inicie una nueva evaluación de directiva después de corregir los problemas de cumplimiento.  


## <a name="see-also"></a>Consulte también

- [Proteger la infraestructura de datos y del sitio con System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Conditional access troubleshooting flow-chart for Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0) (Gráfico del flujo para la solución de problemas de acceso condicional para Configuration Manager)
