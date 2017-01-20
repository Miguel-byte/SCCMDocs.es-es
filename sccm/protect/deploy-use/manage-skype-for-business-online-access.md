---
title: "Administración del acceso a Skype Empresarial Online | System Center Configuration Manager"
description: Aprenda a usar la directiva de acceso condicional para administrar el acceso a Skype Empresarial Online.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3ad36c2-51d4-4467-8bdc-fde18485583e
caps.latest.revision: 6
author: karthikaraman
ms.author: karaman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: a8d0655909c85eb53c2d1eb513586f9733236359


---
# <a name="manage-skype-for-business-online-access"></a>Administrar el acceso de Skype Empresarial Online

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use la directiva de acceso condicional de  **Skype Empresarial Online** para administrar el acceso a esta aplicación en función de las condiciones que especifique.  


 Cuando un usuario determinado intenta usar Skype Empresarial Online en su dispositivo, se produce la siguiente evaluación:![ConditionalAccess&#95;SFBFlow](..//media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Requisitos previos  

-   Habilite la autenticación moderna para Skype Empresarial Online. Cumplimente este [formulario de conexión](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) para inscribirse en el programa de autenticación moderna.  

-   Todos los usuarios finales deben usar Skype Empresarial Online. Si tiene una implementación con Skype Empresarial Online y Skype Empresarial local, no se aplicará la directiva de acceso condicional a los usuarios finales.  

-   El dispositivo que necesita acceso a Skype Empresarial Online debe:  

    -   Ser un dispositivo Android o iOS.  

    -   Estar inscrito con Intune.  

    -   Cumplir todas las directivas de cumplimiento de Intune implementadas.  

 El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso, según las condiciones especificadas.  
Si no se cumple una condición, se presentará al usuario uno de los mensajes siguientes cuando inicie sesión:  

-   Si el dispositivo no está inscrito con Intune, o registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse.  

-   Si el dispositivo no es conforme, se muestra un mensaje que dirige al usuario al sitio web del portal de empresa Intune o a la aplicación del portal de empresa, donde puede encontrar información sobre el problema y sobre cómo resolverlo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configuración de acceso condicional para Skype Empresarial Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Paso 1: Configurar grupos de seguridad de Active Directory  
 Antes de empezar, configure los grupos de seguridad de Azure Active Directory para la directiva de acceso condicional. Puede configurar estos grupos en el Centro de administración de Office 365. Estos grupos contienen los usuarios de destino o exentos de la directiva. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso a los recursos.  

 Puede especificar dos tipos de grupos para utilizarlos con la directiva de Skype Empresarial:  

-   Grupos destinatarios: contiene grupos de usuarios a los que se aplicará la directiva  

-   Grupos exentos: contiene grupos de usuarios que están exentos de la directiva (opcional)  
    Si un usuario pertenece a ambos grupos, estará exento de la directiva.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Paso 2: Configurar e implementar una directiva de cumplimiento  
 Asegúrese de que crea e implementa una directiva de cumplimiento para todos los dispositivos a los que se destinará la directiva de Skype Empresarial Online.  

 Para más información sobre cómo configurar la directiva de cumplimiento, consulte [Administrar directivas de cumplimiento de dispositivo en System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Si no ha implementado una directiva de cumplimiento y luego habilita la directiva de Skype Empresarial Online, se concederá acceso a todos los dispositivos especificados si están inscritos en Intune.  

 Cuando esté listo, continúe en el paso 3.  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Paso 3: Configurar la directiva de Skype Empresarial Online  
 A continuación, configure la directiva para requerir que solo los dispositivos administrados y conformes puedan tener acceso a Skype Empresarial Online. Esta directiva se almacenará en Azure Active Directory.  

1.  En la [consola de administración de Microsoft Intune](https://manage.microsoft.com), haga clic en **Directiva** > **Acceso condicional** > **Skype for Business Online Directiva**.  

     ![ConditionalAccess&#95;SFBPolicy](../media/ConditionalAccess_SFBPolicy.png)  

2.  Seleccione **Habilitar la directiva de acceso condicional**.  

3.  En **Acceso a la aplicación**, puede elegir si desea aplicar la directiva de acceso condicional a:  

    -   iOS  

    -   Android  

4.  En **Grupos de destino**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplicará la directiva. Puede elegir dirigir esto a todos los usuarios o solo a un selecto grupo de usuarios.  

5.  En **Grupos exentos**, opcionalmente, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory que se van a excluir de la directiva.  

6.  Cuando haya terminado, haga clic en **Guardar**.  

 Ya ha configurado el acceso condicional para Skype Empresarial Online. No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Supervisar el cumplimiento y las directivas de acceso condicional  
 En el área de trabajo Grupos, puede ver el estado de acceso condicional de los dispositivos.  

 Seleccione un grupo de dispositivos móviles y, en la pestaña **Dispositivos** , seleccione uno de los siguientes **Filtros**:  

-   **Dispositivos no registrados en AAD**: estos dispositivos están bloqueados en Skype Empresarial Online.  

-   **Dispositivos no conformes**: estos dispositivos están bloqueados en Skype Empresarial Online.  

-   **Dispositivos registrados en AAD y conformes**: estos dispositivos pueden tener acceso a Skype Empresarial Online.  

### <a name="see-also"></a>Consulte también  

 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md) (Administración del acceso a servicios en System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->


