---
title: Configurar la suscripción de Lookout
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar Lookout Mobile Threat Defense.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0946c455732bc13520d3363187b22b118d6e403
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678885"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurar la suscripción con Lookout Mobile Threat Defense

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los pasos siguientes son necesarios para configurar la suscripción de Lookout Mobile Threat Defense:

| #        |Paso  |
| ------------- |-------------|
| 1 | [Recopilar información de Azure AD](#collect-azure-ad-information) |
| 2 | [Configurar la suscripción](#configure-your-subscription) |
| 3 | [Configurar los grupos de inscripción](#configure-enrollment-groups) |
| 4 | [Configurar la sincronización de estado](#configure-state-sync) |
| 5 | [Configurar la información de destinatarios de correo electrónico de informe de errores](#configure-error-report-email-recipient-information) |
| 6 | [Configurar las opciones de inscripción](#configure-enrollment-settings) |
| 7 | [Configurar notificación por correo electrónico](#configure-email-notifications) |
| 8 | [Configurar la clasificación de amenazas](#configure-threat-classification) |
| 9 | [Inspección de la inscripción](#watching-enrollment) |


> [!IMPORTANT]  
> No puede usarse un inquilino de Lookout Mobile Endpoint Security existente que ya no esté asociado con su inquilino de Azure AD para la integración con Azure AD e Intune. Póngase en contacto con el soporte técnico de Lookout para crear un nuevo inquilino de Lookout Mobile Endpoint Security. Use el nuevo inquilino para incorporar sus usuarios de Azure AD.




## <a name="collect-azure-ad-information"></a>Recopilar información de Azure AD
El inquilino de Lookout Mobility Endpoint Security se asociará con su suscripción de Azure AD para integrar Lookout con Intune. Para habilitar la suscripción al servicio de Lookout Mobile Threat Defense, el soporte técnico de Lookout (enterprisesupport@lookout.com) necesita la información siguiente:

- **Id. de inquilino de Azure AD**
- **Id. del objeto de grupo de Azure AD** para el acceso *completo* a la consola de Lookout
- **Id. del objeto de grupo de Azure AD** para el acceso *restringido* a la consola de Lookout (opcional)

Siga estos pasos para recopilar la información que necesita proporcionar al equipo de soporte técnico de Lookout.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) y seleccione su suscripción. 

2. Cuando se elige el nombre de la suscripción, la dirección URL resultante incluye el identificador de la suscripción. Si tiene algún problema para encontrar su id. de suscripción, vea este [artículo de soporte técnico de Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) para obtener sugerencias para buscar su id. de suscripción.

3. Localice el id. de grupo de Azure AD.  
     > [!NOTE]   
     > El **Id. del objeto de grupo** se encuentra en la página **Propiedades** del grupo en la hoja Azure AD de Azure Portal.  

   La consola de Lookout admite dos niveles de acceso:  

   - **Acceso completo:** El Administrador de Azure AD puede crear un grupo para los usuarios que tienen acceso total y, opcionalmente, cree un grupo para los usuarios que tendrán acceso restringido. Solo los usuarios de estos grupos podrán iniciar sesión en la **consola de Lookout**.
   - **Acceso restringido:** Los usuarios de este grupo no tendrá ningún acceso a varias configuración y los módulos relacionados con la inscripción de la consola de Lookout, y tiene acceso de solo lectura a la **directiva de seguridad** módulo de la consola de Lookout.  

     > [!TIP]  
     > Para obtener más información sobre los permisos, consulte [este artículo de soporte técnico de Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Una vez que haya recopilado esta información, póngase en contacto con el soporte técnico de Lookout (correo electrónico: enterprisesupport@lookout.com). El soporte técnico de Lookout trabajará con su contacto principal para incorporar su suscripción y crear su cuenta de Lookout Enterprise, con la información que ha recopilado.



## <a name="configure-your-subscription"></a>Configurar la suscripción

1. Una vez que el servicio de soporte técnico de Lookout crea la cuenta de Lookout Enterprise, Lookout envía un correo electrónico al contacto principal de su empresa con un vínculo a la [dirección URL de inicio de sesión](https://aad.lookout.com/les?action=consent).

2. La primera vez que se inicia sesión en la consola de Lookout para registrar el inquilino de Azure AD, debe usarse una cuenta de usuario con el rol de Administrador global de Azure AD. Los inicios de sesión posteriores no exigirán este nivel de privilegios de Azure AD. Se muestra una página de consentimiento. Pulse **Aceptar** para completar el registro. Una vez que haya aceptado y dado su consentimiento, se le redirige a la consola de Lookout.

   ![captura de pantalla de la página del primer inicio de sesión en la consola de Lookout](media/lookout-initial-login.png)

3. En la [consola de Lookout](https://aad.lookout.com), en el módulo **System** (Sistema), seleccione la pestaña **Connectors** (Conectores) y elija **Intune**.

   ![captura de pantalla de la consola de Lookout con la pestaña Conectores abierta y la opción Intune resaltada](media/lookout-setup-intune-connector.png)

4. Vaya a **Connectors** > **Connection Settings** (Conectores > Configuración de conexión) y especifique en minutos el valor de **Heartbeat Frequency** (Frecuencia de latido).

   ![captura de pantalla de la pestaña de configuración de la conexión que muestra la frecuencia de latido configurada](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurar los grupos de inscripción
1. Para probar la integración de Lookout, se recomienda crear un grupo de seguridad de Azure AD en [Azure Portal](https://portal.azure.com) que contenga un número reducido de usuarios.

    > [!NOTE]  
    > Todos los dispositivos inscritos en Intune que sean compatibles con Lookout, que pertenezcan a usuarios de un grupo de inscripción de Azure AD, y que se identifiquen y admitan en Azure AD, están inscritos y son aptos para la activación en la consola de Lookout MTD.

2. En la [consola de Lookout](https://aad.lookout.com), en el módulo **System** (System), elija la pestaña **Connectors** (Conectores) y seleccione **Enrollment Management** (Administración de inscripciones) para definir un conjunto de usuarios cuyos dispositivos se deban inscribir en Lookout. Agregar el grupo de seguridad de Azure AD **Nombre para mostrar** para su inscripción.

    ![captura de pantalla de la página de inscripción del conector de Intune](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > El **Nombre para mostrar** diferencia entre mayúsculas y minúsculas, tal como se muestra en la página **Propiedades** del grupo de seguridad en Azure Portal. Como se muestra en la imagen siguiente, el **Nombre para mostrar** del grupo de seguridad utiliza mayúsculas y minúsculas, mientras que el título está todo en minúsculas. En la consola de Lookout, las mayúsculas y minúsculas del **Nombre para mostrar** deben coincidir con las del grupo de seguridad.
    >![captura de pantalla de Azure Portal, servicio de Azure Active Directory, página de propiedades](media/aad-group-display-name.png)

    >[!NOTE]  
    >El procedimiento recomendado es usar el valor predeterminado de cinco minutos para el incremento de tiempo a la hora de comprobar si hay nuevos dispositivos. Limitaciones actuales, **Lookout no puede validar los nombres de grupo para mostrar:** Asegúrese del **nombre para mostrar** campo en Azure portal coincide exactamente con el grupo de seguridad de Azure AD. **No se admite la creación de grupos anidados:**  Seguridad de Azure AD grupos que se usan en Lookout solo deben contener usuarios. No pueden contener otros grupos.

3.  Una vez agregado el grupo, la próxima vez que un usuario abre la aplicación Lookout for Work en su dispositivo, el dispositivo se activa en Lookout.

4.  Cuando esté satisfecho con los resultados, amplíe la inscripción a otros grupos de usuarios.



## <a name="configure-state-sync"></a>Configurar la sincronización de estado
En la opción **Sincronización de estado**, especifique el tipo de datos que deben enviarse a Intune. Tanto el estado del dispositivo como el estado de amenaza son necesarios para que la integración de Lookout Intune funcione correctamente. Estas opciones están habilitadas de forma predeterminada.



## <a name="configure-error-report-email-recipient-information"></a>Configurar la información de destinatarios de correo electrónico del informe de errores
En la opción **Administración de errores**, escriba la dirección de correo electrónico que debe recibir los informes de errores.

![captura de pantalla de la página de administración de errores del conector de Intune](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Configurar las opciones de inscripción
En el módulo **Sistema**, en la página **Conectores**, especifique el número de días antes de que un dispositivo se considere como desconectado. Los dispositivos desconectados se consideran como no conformes y se bloqueará su acceso a las aplicaciones de la empresa en función de las directivas de acceso condicional de SCCM. Puede especificar valores entre 1 y 90 días.

![Configuración de la inscripción de Lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurar notificaciones de correo electrónico
Si quiere recibir alertas de correo electrónico para las amenazas, inicie sesión en la [consola de Lookout](https://aad.lookout.com) con la cuenta de usuario que debe recibir las notificaciones. En la pestaña **Preferences** (Preferencias) del módulo **System** (Sistema), seleccione los niveles de amenaza por los que se debería recibir una notificación y **actívelos**. Guarde los cambios.

![captura de pantalla de la página de preferencias con la cuenta de usuario mostrada](media/lookout-email-notifications.png) Si ya no quiere recibir notificaciones de correo electrónico, desactive las notificaciones y guarde los cambios.



## <a name="configure-threat-classification"></a>Configurar la clasificación de amenazas
Lookout Mobile Threat Defense clasifica las amenazas móviles en varios tipos. Las [clasificaciones de amenazas de Lookout](http://personal.support.lookout.com/hc/articles/114094130693) tienen niveles de riesgo predeterminados asociados a ellos. Esta configuración puede cambiarse en cualquier momento para adaptarse a los requisitos de la empresa.

![captura de pantalla de la página de directivas que muestra las amenazas y las clasificaciones](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> Los niveles de riesgo son un aspecto importante en la defensa contra las amenazas móviles. La integración de Intune calcula la conformidad de los dispositivos en tiempo de ejecución según estos niveles de riesgo. El administrador de Intune establece una regla en la directiva para identificar un dispositivo como no conforme si este tiene una amenaza activa con un nivel mínimo de: **alto**, **medio** o **bajo**. La directiva de clasificación de amenazas en Lookout Mobile Threat Defense realiza directamente el cálculo de conformidad del dispositivo en Intune.



## <a name="watching-enrollment"></a>Inspección de la inscripción
Una vez que se ha completado la configuración, Lookout Mobile Threat Defense comienza a sondear Azure AD en busca de los dispositivos que se corresponden con los grupos de inscripción especificados. Puede encontrar información sobre los dispositivos inscritos en el módulo Dispositivos. El estado inicial de los dispositivos se muestra como pendiente. El estado del dispositivo cambia una vez que la aplicación Lookout for Work se instala, se abre y se activa en el dispositivo. Para obtener más información sobre cómo conseguir que la aplicación Lookout for Work se inserte en el dispositivo, vea el tema [Configurar e implementar aplicaciones Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Pasos siguientes
[Enable Lookout MTP connection in Intune (Habilitar la conexión de Lookout MTP en Intune)](enable-lookout-connection-in-intune.md)
