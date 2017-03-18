---
title: "Configurar su suscripción con Lookout| System Center Configuration Manager"
description: "En este tema se proporciona información sobre cómo configurar la protección contra amenazas de dispositivo de Lookout."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2d01b6d327e98a433030faebbff8f80fa6a8f48e
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configurar su suscripción para la protección contra amenazas de dispositivo de Lookout

*Se aplica a: System Center Configuration Manager (rama actual)*

Para tener preparada su suscripción para el servicio de protección contra amenazas de dispositivo de Lookout, el soporte técnico de Lookout (enterprisesupport@lookout.com) necesita la siguiente información sobre su suscripción de Azure Active Directory (Azure AD). El inquilino de Lookout Mobility Endpoint Security se asociará con su suscripción de Azure AD para integrar Lookout con Intune. 

* **Id. de inquilino de Azure AD**
* **Id. del objeto de grupo de Azure AD** para el acceso **completo** a la consola de Lookout
* **Id. del objeto de grupo de Azure AD** para el acceso **restringido** a la consola de Lookout (opcional)

> [!IMPORTANT]
> No puede usarse un inquilino de Lookout Mobile Endpoint Security existente que ya no esté asociado con su inquilino de Azure AD para la integración con Azure AD e Intune. Póngase en contacto con el soporte técnico de Lookout para crear un nuevo inquilino de Lookout Mobile Endpoint Security. Use el nuevo inquilino para incorporar sus usuarios de Azure AD.

Use la siguiente sección para recopilar la información que necesita proporcionar al equipo de soporte técnico de Lookout.  

## <a name="get-your-azure-ad-information"></a>Obtener la información de Azure AD
### <a name="azure-ad-tenant-id"></a>Id. de inquilino de Azure AD
Inicie sesión en el [Portal de administración de Azure AD](https://manage.windowsazure.com) y seleccione su suscripción. 

![captura de pantalla de la página de Azure AD que muestra el nombre del inquilino](media/aad_tenant_name.png) Cuando elige el nombre de la suscripción, la dirección URL resultante incluye el id. de suscripción.  Si tiene algún problema para encontrar su id. de suscripción, vea este [artículo de soporte técnico de Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) para obtener sugerencias para buscar su id. de suscripción.   
### <a name="azure-ad-group-id"></a>Id. de grupo de Azure AD
La consola de Lookout admite dos niveles de acceso:  
* **Acceso completo:** el administrador de Azure AD puede crear un grupo para usuarios que tengan acceso completo y, opcionalmente, crear un grupo de usuarios que tengan acceso restringido.  Solo los usuarios de estos grupos podrán iniciar sesión en la **consola de Lookout**.
* **Acceso restringido:** los usuarios de este grupo no tendrán acceso a varios módulos relacionados con la inscripción y configuración de la consola de Lookout, y tendrán acceso de solo lectura al módulo **Directiva de seguridad** de la consola de Lookout.  

Para obtener más detalles sobre los permisos, lea [este artículo](https://personal.support.lookout.com/hc/en-us/articles/114094105653) en el sitio web de Lookout.

El **Id. del objeto de grupo** se encuentra en la página **Propiedades** del grupo en la **consola de administración de Azure AD**.

![captura de pantalla de la página de propiedades con el campo de id. de grupo resaltado](media/aad_group_object_id.png)

Una vez que haya recopilado esta información, póngase en contacto con el soporte técnico de Lookout (correo electrónico: enterprisesupport@lookout.com).

El soporte técnico de Lookout trabajará con su contacto principal para incorporar su suscripción y crear su cuenta de Lookout Enterprise, con la información que ha recopilado.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configurar su suscripción con la protección contra amenazas de dispositivo de Lookout
### <a name="step-1-set-up-your-device-threat-protection"></a>Paso 1: Configurar la protección contra amenazas de dispositivo
Después de que el equipo de soporte técnico de Lookout cree su cuenta de Lookout Enterprise, puede iniciar sesión en la consola de Lookout.   Se envía un correo electrónico de Lookout al contacto principal de su empresa con un vínculo a la dirección URL de inicio de sesión: https://aad.lookout.com/les?action=consent

Debe usar una cuenta de usuario con el rol de Administrador global de Azure AD cuando inicie sesión por primera vez en la consola de Lookout, ya que Lookout necesita esta información para registrar su inquilino de Azure AD.   Los inicios de sesión posteriores no necesitarán que el usuario tenga este nivel de privilegio de Azure AD.  En el primer inicio de sesión, se muestra una página de consentimiento. Pulse **Aceptar** para completar el registro.

![captura de pantalla de la página del primer inicio de sesión en la consola de Lookout](media/lookout-initial-login.png)

Una vez que haya aceptado y dado su consentimiento, se le redirige a la consola de Lookout. Los inicios de sesión posteriores después del registro inicial pueden realizarse con la dirección URL: https://aad.lookout.com

Vea el [artículo de solución de problemas]() si tiene problemas de inicio de sesión.

En los siguientes pasos se detallan las tareas que debe realizar para completar la configuración de Lookout en la [consola de Lookout](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Paso 2: Configurar el conector de Intune

1.  En la consola de Lookout, en el módulo **Sistema**, pulse la pestaña **Conectores** y seleccione **Intune**.

  ![captura de pantalla de la consola de Lookout con la pestaña Conectores abierta y la opción Intune resaltada](media/lookout-setup-intune-connector.png)

2.  En la opción de configuración de la conexión, configure la frecuencia de latido en minutos.  Su conector de Intune ya está listo.  

  ![captura de pantalla de la pestaña de configuración de la conexión que muestra la frecuencia de latido configurada](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Paso 3: Configurar los grupos de inscripción
En la opción **Administración de inscripciones**, defina un conjunto de usuarios cuyos dispositivos deben inscribirse con Lookout. El procedimiento recomendado es empezar con un grupo de usuarios pequeño para probar y familiarizarse con el funcionamiento de la integración.  Una vez que esté satisfecho con los resultados de prueba, puede ampliar la inscripción a grupos de usuarios adicionales.

Para comenzar con los grupos de inscripción, primero defina un grupo de seguridad de Azure AD, que sería un buen primer conjunto de usuarios que se va a inscribir en la protección contra amenazas de dispositivo de Lookout. Una vez que tenga el grupo creado en Azure AD, en la consola de Lookout, vaya a la opción **Administración de inscripciones** y agregue el **Nombre para mostrar** del grupo de seguridad de Azure AD para la inscripción.

Cuando un usuario se encuentra en un grupo de inscripción, cualquiera de sus dispositivos que se identifica y se admite en Azure AD está inscrito y es apto para la activación de la protección contra amenazas de dispositivo de Lookout.  La primera vez que abre la aplicación Lookout for Work en su dispositivo compatible, el dispositivo se activa en Lookout.

![captura de pantalla de la página de inscripción del conector de Intune](media/lookout-enrollment.png)

El procedimiento recomendado es usar el valor predeterminado (5 minutos) para el incremento de tiempo a la hora de comprobar nuevos dispositivos.

>[!IMPORTANT]
> El nombre para mostrar distingue mayúsculas de minúsculas.  Use el **Nombre para mostrar** como se muestra en la página **Propiedades** del grupo de seguridad en Azure Portal. Tenga en cuenta en la imagen siguiente que en la página **Propiedades** del grupo de seguridad, el nombre para mostrar alterna mayúsculas y minúsculas.  En cambio, el título se muestra en minúsculas y no debe usarse para escribir en la consola de Lookout.
>![captura de pantalla de Azure Portal, servicio de Azure Active Directory, página de propiedades](media/aad-group-display-name.png)

La versión actual tiene las siguientes limitaciones:  
* No hay ninguna validación para los nombres para mostrar del grupo.  Asegúrese de usar el valor del campo **NOMBRE PARA MOSTRAR** que se muestra en Azure Portal para el grupo de seguridad de Azure AD.
* La creación de grupos dentro de grupos no se admite en estos momentos.  Los grupos de seguridad de Azure AD especificados solo pueden contener usuarios y no grupos anidados.


### <a name="step-4-configure-state-sync"></a>Paso 4: Configurar la sincronización de estado
En la opción **Sincronización de estado**, especifique el tipo de datos que deben enviarse a Intune.  Actualmente, debe habilitar el estado del dispositivo y el estado de amenaza para que la integración de Lookout Intune funcione correctamente.  Están habilitados de manera predeterminada.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Paso 5: Configurar la información de destinatarios de correo electrónico de informe de errores
En la opción **Administración de errores**, escriba la dirección de correo electrónico que debe recibir los informes de errores.

![captura de pantalla de la página de administración de errores del conector de Intune](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Paso 6. Configurar las opciones de inscripción
En el módulo **Sistema**, en la página **Conectores**, especifique el número de días antes de que un dispositivo se considere como desconectado.  Los dispositivos desconectados se consideran como no conformes y se bloquearán del acceso a las aplicaciones de la empresa en función de las directivas de acceso condicional de SCCM. Puede especificar valores entre 1 y 90 días.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Paso 7: Configurar notificaciones de correo electrónico
Si quiere recibir alertas de correo electrónico para las amenazas, inicie sesión en la [consola de Lookout](https://aad.lookout.com) con la cuenta de usuario que debe recibir las notificaciones. En la pestaña **Preferencias** del módulo **Sistema**, pulse las notificaciones deseadas y establézcalas como **ACTIVADA**. Guarde los cambios.

![captura de pantalla de la página de preferencias con la cuenta de usuario mostrada](media/lookout-email-notifications.png) Si ya no quiere recibir notificaciones de correo electrónico, establezca las notificaciones en **DESACTIVADA** y guarde los cambios.
### <a name="step-8-configure-threat-classification"></a>Paso 8: Configurar la clasificación de amenazas
La protección contra amenazas de dispositivo de Lookout clasifica las amenazas móviles en varios tipos. Las [clasificaciones de amenazas de Lookout](http://personal.support.lookout.com/hc/en-us/articles/114094130693) tienen niveles de riesgo predeterminados asociados a ellos. Estos pueden cambiarse en cualquier momento para adaptarse a los requisitos de la empresa.

![captura de pantalla de la página de directivas que muestra las amenazas y las clasificaciones](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Los niveles de riesgo que se han especificado aquí son un aspecto importante de la protección contra amenazas de dispositivo porque la integración en Intune calcula el cumplimiento del dispositivo según estos niveles de riesgo en tiempo de ejecución. En otras palabras, el administrador de Intune establece una regla en la directiva para identificar un dispositivo como no conforme si este tiene una amenaza activa con un nivel mínimo de: alto, medio o bajo. La directiva de clasificación de amenazas en la protección contra amenazas de dispositivo de Lookout realiza directamente el cálculo de cumplimiento del dispositivo en Intune.

## <a name="watching-enrollment"></a>Inspección de la inscripción
Una vez que se ha completado la configuración, la protección contra amenazas de dispositivo de Lookout comienza a sondear Azure AD para los dispositivos que se corresponden con los grupos de inscripción especificados.  Puede encontrar información sobre los dispositivos inscritos en el módulo Dispositivos.  El estado inicial de los dispositivos se muestra como pendiente.  El estado del dispositivo cambia una vez que la aplicación Lookout for Work se instala, se abre y se activa en el dispositivo.  Para obtener información sobre cómo obtener que la aplicación Lookout for Work se inserte en el dispositivo, vea el tema [Configure and deploy Lookout for work apps (Configurar e implementar aplicaciones Lookout for Work)](configure-and-deploy-lookout-for-work-apps.md).
## <a name="next-steps"></a>Pasos siguientes
[Enable Lookout MTP connection in Intune (Habilitar la conexión de Lookout MTP en Intune)](enable-lookout-connection-in-intune.md)

