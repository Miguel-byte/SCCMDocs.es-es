---
title: Administrar el acceso a servicios de O365 para equipos administrados | Microsoft Docs
description: Aprenda a configurar el acceso condicional para equipos administrados por System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: 15
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: b7c55ce5629565cb1e3aede6680ef1796f56cb20
ms.lasthandoff: 03/06/2017


---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Administración del acceso a servicios de O365 para equipos administrados por System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



 A partir de la versión 1602 de Configuration Manager, puede configurar el acceso condicional para equipos administrados por System Center Configuration Manager.  

> [!IMPORTANT]  
>  Se trata de una característica de versión preliminar disponible en las actualizaciones 1602, 1606 y 1610. Se incluyen características de versión preliminar en el producto para la realización de las primeras pruebas en un entorno de producción, pero no se debe considerar que ya estén listas para él. Para más información, consulte [Use pre-release features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease) (Uso de características de la versión preliminar a partir de las actualizaciones).
> - Después de instalar la actualización 1602, el tipo de característica aparece como publicado, aunque se trate de una versión preliminar.
> - Si actualiza de la versión 1602 a la 1606, el tipo de característica se muestra como liberado aunque se conserve la versión preliminar.
> - Si actualiza de la versión 1511 directamente a la versión 1606, el tipo de característica se muestra como versión preliminar.

 Si desea obtener información sobre cómo configurar el acceso condicional para dispositivos inscritos y administrados por Intune o equipos que están unidos a un dominio y cuya compatibilidad no se evalúa, consulte [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a servicios en System Center Configuration Manager).  


## <a name="supported-services"></a>Servicios compatibles  

-   Exchange Online  

-   SharePoint Online  

## <a name="supported-pcs"></a>Equipos compatibles  

-   Windows 7  

-   Windows 8.1  

-   Windows 10 todavía no es totalmente compatible.  Si intenta establecer el acceso condicional para equipos Windows 10, se pueden producir algunos problemas.  Consulte [Problemas conocidos](#bkmk_KnownIssues) para obtener información detallada.  

## <a name="configure-conditional-access"></a>Configuración de acceso condicional  
 Para configurar el acceso condicional, primero debe crear una directiva de cumplimiento y configurar la directiva de acceso condicional. Al configurar las directivas de acceso condicional para equipos, puede requerir que los equipos se atengan a la directiva de cumplimiento para acceder a los servicios Exchange Online y SharePoint Online.  

### <a name="prerequisites"></a>Requisitos previos  

-   Sincronización de ADFS y una suscripción de O365. La suscripción de Office&365; sirve para configurar Exchange Online y SharePoint Online.  

-   Suscripción a Microsoft Intune. La suscripción a Microsoft Intune debe configurarse en la consola de Configuration Manager. Esto todavía requiere que se disponga de una implementación híbrida.  

 Los equipos deben cumplir los requisitos siguientes:  

-   [Requisitos previos](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1) para el registro automático de dispositivos con Azure Active Directory  

     Puede registrar equipos con Azure AD a través de la directiva de cumplimiento.  

    -   Para equipos con Windows 8.1 y Windows 10, puede usar una directiva de grupo de Active Directory para configurar los dispositivos a fin de que se registren automáticamente en Azure AD.  

    -   Para equipos con Windows 7, debe implementar el paquete de software de registro de dispositivo en el equipo con Windows 7 a través de System Center Configuration Manager. Puede encontrar más información en el tema [Registro automático de dispositivos en Azure Active Directory para dispositivos Windows unidos a un dominio](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

-   Debe usar Office 2013 u Office 2016 con la autenticación moderna [habilitada](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 Los pasos descritos a continuación se aplican a Exchange Online y SharePoint Online.  

### <a name="step-1-configure-compliance-policy"></a>Paso 1. Configurar directiva de cumplimiento  
 En la consola de Configuration Manager, cree una directiva de cumplimiento con las reglas siguientes:  

-   Requerir registro en Azure Active Directory: esta regla comprueba si el dispositivo del usuario está unido al lugar de trabajo en Azure AD; de lo contrario, el dispositivo se registra automáticamente en Azure AD. El registro automático solo se admite en Windows 8.1. Para equipos con Windows 7, implemente un archivo MSI para realizar el registro automático. Para más información, consulte [Registro automático de dispositivos en Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

-   **Todas las actualizaciones necesarias que se instalan con una fecha límite anterior a un número determinado de días**: esta regla comprueba si el dispositivo del usuario tiene todas las actualizaciones necesarias (especificadas en la regla Actualizaciones automáticas requeridas) dentro de la fecha límite y el período de gracia que usted especifique e instala automáticamente cualquier actualización necesaria pendiente.  

-   **Requerir cifrado de unidad BitLocker**: se trata de una comprobación para ver si la unidad principal (por ejemplo, C:\\\) del dispositivo está cifrada con BitLocker. Si el cifrado BitLocker no está habilitado en el dispositivo primario, se bloquea el acceso a los servicios de correo electrónico y SharePoint.  

-   **Requerir antimalware:** se trata de una comprobación para ver si el software antimalware (System Center Endpoint Protection o Windows Defender solamente) está habilitado y en ejecución. Si no está habilitado, se bloquea el acceso a los servicios de correo electrónico y SharePoint.  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Paso 2. Evaluar el impacto del acceso condicional  
 Ejecute el informe de compatibilidad de acceso condicional. Se puede encontrar en la sección Supervisión, en Informes > Administración de compatibilidad y configuración. Esto muestra el estado de cumplimiento para todos los dispositivos.  Se bloqueará el acceso de los dispositivos registrados como no compatibles a Exchange Online y SharePoint Online.  

 ![CA&#95;compliance&#95;report](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurar grupos de seguridad de Active Directory  
 Las directivas de acceso condicional se dirigen a grupos de usuarios en función de los tipos de directivas. Estos grupos contienen los usuarios de destino o exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso al servicio.  

 Grupos de usuarios de seguridad de Active Directory Estos grupos de usuarios se deben sincronizar con Azure Active Directory. Estos grupos se pueden configurar también en el Centro de administración de Office 365 o en el Portal de cuentas de Intune.  

 Se pueden especificar dos tipos de grupo en cada directiva. :  

-   **Grupos destinatarios**: grupos de usuarios a los que se aplica la directiva. Debe usarse el mismo grupo para la directiva de cumplimiento y de acceso condicional.  

-   **Grupos exentos**: grupos de usuarios que están exentos de la directiva (opcional)  
    Si un usuario pertenece a ambos, estará exento de la directiva.  

     Solo se evalúan los grupos que son destinatarios de la directiva de acceso condicional.  

### <a name="step-3--create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Paso 3.  Crear una directiva de acceso condicional para Exchange Online y SharePoint Online  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  Para crear una directiva para Exchange Online, seleccione **Habilitar directiva de acceso condicional para Exchange Online**.  

     Para crear una directiva para SharePoint Online, seleccione **Habilitar directiva de acceso condicional para Exchange Online**.  

3.  En la pestaña **Inicio** , en el grupo **Vínculos** , haga clic en **Configurar directiva de acceso condicional en la consola de Intune**. Puede que deba proporcionar el nombre de usuario y la contraseña de la cuenta utilizada para conectar Configuration Manager con Intune.  

     Se abrirá la consola de administración de Intune.  

4.  Para Exchange Online, en la consola de administración de Microsoft Intune, haga clic en **Directiva > Acceso condicional > Directiva de Exchange Online**.  

     Para SharePoint Online, en la consola de administración de Microsoft Intune, haga clic en **Directiva > Acceso condicional > Directiva de SharePoint Online**.  

5.  Defina el requisito de equipos Windows con la opción**Los dispositivos deben ser compatibles**.  

6.  En **Grupos de destino**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplicará la directiva.  

    > [!NOTE]  
    >  Debe usarse el mismo grupo de usuarios de seguridad para implementar la directiva de cumplimiento y el grupo de destino de la directiva de acceso condicional.  

     En **Grupos exentos**, opcionalmente, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory que se van a excluir de la directiva.  

7.  Haga clic en **Guardar** para crear y guardar la directiva.  

 Los usuarios finales que están bloqueados debido a la falta de cumplimiento van a ver información de cumplimiento en el Centro de software de System Center Configuration Manager e iniciarán una nueva evaluación de directivas cuando se corrijan los problemas de cumplimiento.  

##  <a name="bkmk_KnownIssues"></a> Problemas conocidos  
 Puede ver los siguientes problemas al utilizar esta característica:  

-   En esta actualización 1602, no se exige el cumplimiento de 5 días. Incluso si la comprobación de cumplimiento en el dispositivo del usuario final se produjo hace más de 5 días, los usuarios todavía pueden acceder a Office 365 y SharePoint Online.  

-   Cuando un dispositivo no es compatible con la directiva de cumplimiento, el motivo no se muestra automáticamente. El usuario final debe ir al Centro de software nuevo para averiguar el motivo de la no conformidad. El motivo se muestra en la sección Conformidad de dispositivos del Centro de software.  

-   Los usuarios de Windows 10 pueden ver varios errores de acceso al intentar tener acceso a recursos de Office 365 y SharePoint Online. Tenga en cuenta que el acceso condicional no se admite totalmente para Windows 10.  

### <a name="see-also"></a>Consulte también  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md) (Proteger la infraestructura de datos y del sitio con System Center Configuration Manager)

