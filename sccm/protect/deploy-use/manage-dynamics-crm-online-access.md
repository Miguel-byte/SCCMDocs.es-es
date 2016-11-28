---
title: "Administración del acceso a Dynamics CRM Online | System Center Configuration Manager"
description: Aprenda a controlar el acceso a Microsoft Dynamics CRM Online desde los dispositivos de iOS y Android con el acceso condicional de Microsoft Intune.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7cec31-f78d-46b9-93ae-a12ae27a1de6
caps.latest.revision: 5
author: karthikaraman
ms.author: karaman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5c6cf3c1697b49708aa5192b67b08b700da7dc72
ms.openlocfilehash: 61409cf78bef3991d096c5c9615ff667aca9cb43

---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Administración del acceso a Dynamics CRM Online en System Center Configuration Manager.

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede controlar el acceso a Microsoft Dynamics CRM Online desde los dispositivos de iOS y Android con el acceso condicional de Microsoft Intune.  El acceso condicional de Intune tiene dos componentes:
* [La directiva de cumplimiento del dispositivo](../../protect/deploy-use/device-compliance-policies.md), con la que debe cumplir el dispositivo para que se considere compatible.
* [La directiva de acceso condicional](../../protect/deploy-use/manage-access-to-services.md), donde se especifican las condiciones que debe cumplir el dispositivo para tener acceso al servicio.

Para más información sobre cómo funciona el acceso condicional, vea el artículo [Manage access to services](../../protect/deploy-use/manage-access-to-services.md) (Administración del acceso a los servicios).


Cuando un usuario determinado intenta usar la aplicación Dynamics CRM en su dispositivo, se produce la siguiente evaluación:

![Diagrama que muestra los puntos de decisión usados para determinar si un dispositivo puede tener acceso a un servicio o si se bloquea.](../media/mdm-ca-dynamics-crm-flow-diagram.png)

El dispositivo que necesita tener acceso a Dynamics CRM Online:
* Debe ser un dispositivo **Android** o **iOS**.
* Debe estar **inscrito** en Microsoft Intune.
* Debe **cumplir** todas las directivas de cumplimiento de Microsoft Intune implementadas.

El estado del dispositivo se almacena en Azure Active Directory, que concede o bloquea el acceso, según las condiciones especificadas.

Si no se cumple una condición, se presentará al usuario uno de los mensajes siguientes cuando inicie sesión:
* Si el dispositivo no está inscrito en Microsoft Intune o registrado en Azure Active Directory, se muestra un mensaje con instrucciones sobre cómo instalar la aplicación de portal de empresa e inscribirse.
* Si el dispositivo no es compatible, se muestra un mensaje que dirige al usuario al sitio web de portal de empresa de Microsoft Intune o a la aplicación de portal de empresa, donde puede encontrar información sobre el problema y sobre cómo resolverlo.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configuración de un acceso condicional para Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Paso 1: Configurar grupos de seguridad de Active Directory

Antes de empezar, configure los grupos de seguridad de Azure Active Directory para la directiva de acceso condicional. Estos grupos se pueden configurar en el **Centro de administración de Office 365**. Estos grupos se usarán para aplicar la directiva a los usuarios o para excluirlos de ella. Cuando un usuario es destinatario de una directiva, cada dispositivo que use debe ser conforme con el fin de obtener acceso a los recursos.

Puede especificar dos tipos de grupos para usarlos con la directiva de Dynamics CRM:
* **Grupos de destino**: contiene grupos de usuarios a los que se aplicará la directiva.
* **Grupos exentos**: contiene grupos de usuarios que están exentos de la directiva.

Si un usuario pertenece a ambos grupos, estará exento de la directiva.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Paso 2: Configurar e implementar una directiva de cumplimiento
[Cree e implemente](../../protect/deploy-use/device-compliance-policies.md) una directiva de cumplimiento para todos los dispositivos que se verán afectados por la directiva. Dichos dispositivos serán los que usen los usuarios de los Grupos de destino.

> [!NOTE]
> Mientras que las directivas de cumplimiento se implementan en los grupos de Microsoft Intune, las directivas de acceso condicional se aplican a los grupos de seguridad de Azure Active Directory.

> [!IMPORTANT]
> Si no ha implementado una directiva de cumplimiento, los dispositivos se considerarán no conformes.

Cuando esté listo, continúe en el paso 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Paso 3: Configurar la directiva de Dynamics CRM
A continuación, configure la directiva para requerir que solo los dispositivos administrados y compatibles puedan tener acceso a Dynamics CRM. Esta directiva se almacenará en Azure Active Directory.

1.  En la consola de administración de Microsoft Intune, elija **Directiva > Acceso condicional > Directiva de Dynamics CRM Online**.

     ![Captura de pantalla de la página de la directiva de acceso condicional de Dynamics CRM Online](../media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  Seleccione **Habilitar la directiva de acceso condicional**.
3.  En **Acceso a la aplicación**, puede elegir si desea aplicar la directiva de acceso condicional a:
  * **iOS**
  * **Android**
4.  En **Grupos de destino**, seleccione **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory a los que se aplicará la directiva. Puede elegir dirigir esto a todos los usuarios o solo a un selecto grupo de usuarios.
5.  En **Grupos exentos**, opcionalmente, elija **Modificar** para seleccionar los grupos de seguridad de Azure Active Directory exentos de esta directiva.
6.  Cuando termine, elija **Guardar**.

Acaba de configurar el acceso condicional para Dynamics CRM. No es necesario implementar la directiva de acceso condicional, ya que surte efecto inmediatamente.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>Supervisar el cumplimiento y las directivas de acceso condicional

En el área de trabajo **Grupos**, puede ver el estado de acceso condicional de los dispositivos.

Seleccione un grupo de dispositivos móviles y, en la pestaña **Dispositivos** , seleccione uno de los siguientes **Filtros**:
* **Dispositivos no registrados en AAD**: estos dispositivos están bloqueados en Dynamics CRM.
* **Dispositivos no compatibles**: estos dispositivos están bloqueados en Dynamics CRM.
* **Dispositivos registrados en AAD y compatibles**: estos dispositivos pueden tener acceso a Dynamics CRM.

###  <a name="see-also"></a>Consulte también
[Manage access to email](../../protect/deploy-use/manage-email-access.md) (Administración del acceso al correo electrónico)

[Manage access to SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md) (Administración del acceso a SharePoint Online)

[Manage access to Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md) (Administración del acceso a Skype Empresarial Online)



<!--HONumber=Nov16_HO1-->


