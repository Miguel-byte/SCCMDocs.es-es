---
title: Administrar el acceso de Skype Empresarial Online
titleSuffix: Configuration Manager
description: Aprenda a usar la directiva de acceso condicional para administrar el acceso a Skype Empresarial Online.
ms.custom: na
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 3c1d0c84dc28fb886048cf8d7ea310c2b4dfc4aa
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="manage-skype-for-business-online-access"></a>Administrar el acceso de Skype Empresarial Online

*Se aplica a: System Center Configuration Manager (Rama actual)*


Use la directiva de acceso condicional de Skype Empresarial Online para administrar el acceso a esta aplicación en función de las condiciones que especifique.  


 Cuando un usuario determinado intenta usar Skype Empresarial Online en su dispositivo, se produce la siguiente evaluación:![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Requisitos previos  

-   Habilite la [autenticación moderna](https://aka.ms/SkypeModernAuth) para Skype Empresarial Online.   

-   Todos los usuarios deben usar Skype Empresarial Online. Si tiene una implementación con Skype Empresarial Online y Skype Empresarial local, la directiva de acceso condicional no se aplica a los usuarios locales.  

-   El dispositivo que necesita acceso a Skype Empresarial Online debe:  

    -   Debe ser un dispositivo Android o iOS

    -   Debe estar inscrito en Microsoft Intune

    -   Debe cumplir todas las directivas de cumplimiento de Microsoft Intune implementadas

 El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso según las condiciones especificadas.  
Si no se cumple una condición, el usuario ve uno de los mensajes siguientes cuando inicie sesión:  

-   Si el dispositivo no está inscrito en Microsoft Intune o registrado en Azure Active Directory, el usuario ve instrucciones sobre cómo instalar la aplicación Portal de empresa e inscribirse.  

-   Si el dispositivo no es conforme, el usuario ve un mensaje que le dirige al sitio web o a la aplicación Portal de empresa. El Portal de empresa tiene información sobre el problema y cómo resolverlo.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configuración de acceso condicional para Skype Empresarial Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Paso 1: Configurar grupos de seguridad de Active Directory  
 Antes de empezar, configure los grupos de seguridad de Azure Active Directory para la directiva de acceso condicional. Configure estos grupos en el Centro de administración de Office 365. Estos grupos contienen los usuarios a los que se destina la directiva o que se excluyen de ella. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso a los recursos.  

 Puede especificar dos tipos de grupos para utilizarlos con la directiva de Skype Empresarial:  

-   Los **Grupos destinatarios** contienen los usuarios a los que se aplica la directiva  

-   Los **Grupos exentos** contienen los usuarios que se excluyen de la directiva  
    Si un usuario pertenece a ambos grupos, estará exento.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Paso 2: Configurar e implementar una directiva de cumplimiento  
 Cree e implemente una directiva de cumplimiento para todos los dispositivos a los que se destina la directiva de Skype Empresarial Online.  

 Para obtener más información sobre cómo configurar la directiva de cumplimiento, vea [Administración de directivas de cumplimiento del dispositivo](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Si no ha implementado una directiva de cumplimiento y luego habilita la directiva de Skype Empresarial Online, se concede acceso a todos los dispositivos especificados si están inscritos en Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Paso 3: Configurar la directiva de Skype Empresarial Online  
 Configure la directiva para requerir que solo los dispositivos administrados y conformes puedan tener acceso a Skype Empresarial Online. Esta directiva se almacena en Azure Active Directory.  

1.  En la [consola de administración de Microsoft Intune](https://manage.microsoft.com), haga clic en **Directiva** > **Acceso condicional** > **Skype for Business Online Directiva**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Seleccione **Habilitar la directiva de acceso condicional**.  

3.  En **Acceso a la aplicación**, puede elegir si desea aplicar la directiva de acceso condicional a:  

    -   iOS  

    -   Android  

4.  En **Grupos destinatarios**, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplica la directiva. Puede elegir dirigir esta directiva a todos los usuarios o solo a un grupo selecto de usuarios.  

5.  En **Grupos exentos**, opcionalmente, haga clic en **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory que se van a excluir de la directiva.  

6.  Cuando haya terminado, haga clic en **Guardar**.  

 Ya ha configurado el acceso condicional para Skype Empresarial Online. No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>Supervisar el cumplimiento y las directivas de acceso condicional  
 En el área de trabajo Grupos, puede ver el estado de acceso condicional de los dispositivos.  

 Seleccione un grupo de dispositivos móviles y, en la pestaña **Dispositivos** , seleccione uno de los siguientes **Filtros**:  

-   Los **Dispositivos no registrados en AAD** están bloqueados en Skype Empresarial Online

-   Los **Dispositivos no conformes** están bloqueados en Skype Empresarial Online  

-   Los **Dispositivos registrados en AAD y conformes** pueden tener acceso a Skype Empresarial Online  

### <a name="see-also"></a>Consulte también  

 [Manage access to services in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md) (Administración del acceso a servicios en System Center Configuration Manager)
