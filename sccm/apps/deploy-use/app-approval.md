---
title: Aprobar aplicaciones
titleSuffix: Configuration Manager
description: Obtenga información sobre la configuración y los comportamientos de la aprobación de aplicaciones en Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a650fd5517fb86108d230cc997c8586520826e7
ms.sourcegitcommit: 16dd488c51b5cf01a7dd4204f7d40ee9ae0abe85
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2019
ms.locfileid: "68743579"
---
# <a name="approve-applications-in-configuration-manager"></a>Aprobar aplicaciones en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Al [implementar una aplicación](/sccm/apps/deploy-use/deploy-applications) en Configuration Manager, se puede necesitar su aprobación antes de instalarla. Los usuarios solicitan la aplicación en el Centro de software y la solicitud se revisa en la consola de Configuration Manager. La solicitud se puede aprobar o denegar.

## <a name="bkmk_approval"></a> Configuración de aprobación

El comportamiento de aprobación de la aplicación depende de si habilita la [experiencia de aprobación de aplicación opcional](#bkmk_opt)recomendada. En la página **Configuración de implementación** de la implementación de aplicaciones aparece una de las siguientes opciones de aprobación:  

### <a name="bkmk_opt"></a> Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo

> [!Note]  
> Configuration Manager no habilita esta característica de forma predeterminada. Antes de usarla, habilite la característica opcional **Aprobar solicitudes de aplicación de usuarios por dispositivo**. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).
>
> Si no habilita esta característica, verá la [experiencia anterior](#bkmk_prior).  

El administrador aprueba las solicitudes de usuario sobre la aplicación para que el usuario pueda instalarla en el dispositivo solicitado. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos. <!--1357015-->  

> [!Note]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.<!--SCCMDocs issue 646-->  

Vea **Solicitudes de aplicación** en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** de la consola de Configuration Manager. (En la versión 1902 y versiones anteriores, este nodo se denomina **solicitudes de aprobación**). Hay una columna **Dispositivo** en la lista de cada solicitud. Al realizar acciones en la solicitud, el cuadro de diálogo Solicitud de aplicación también incluye el nombre del dispositivo desde el que el usuario envió la solicitud.

Si una solicitud no se aprueba antes de 30 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

Cuando se requiere la aprobación de una implementación en una recopilación de dispositivos, la aplicación no se muestra en el centro de software. Si necesita aprobación en una implementación en una recopilación de usuarios, la aplicación se muestra en el centro de software. Todavía puede ocultarla de los usuarios con la configuración de cliente, **ocultar aplicaciones no aprobadas en el centro de software**. Para obtener más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#software-center).

Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  

> [!Important]  
> A partir de la versión 1806, *el comportamiento ha cambiado* al revocar la aprobación de una aplicación que se haya aprobado e instalado anteriormente. Ahora, al **Denegar** la solicitud de la aplicación, el cliente desinstala la aplicación del dispositivo del usuario.<!--1357891-->  

A partir de la versión 1906, si aprueba una solicitud de aplicación en la consola y después la deniega, ahora la puede volver a aprobar. Después de que apruebe la aplicación, se vuelve a instalar en el cliente.  <!-- 4224910 -->

Automatice el proceso de aprobación con el cmdlet [Approve-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) de PowerShell. A partir de la versión 1902, este cmdlet incluye el parámetro **InstallActionBehavior**. Use este parámetro para especificar si quiere instalar la aplicación de inmediato o fuera del horario laboral.<!-- SCCMDocs-pr issue #3418 -->

A partir de 1906, puede ver qué implementaciones requieren aprobación. Seleccione una aplicación en el nodo **aplicaciones** . En el panel de detalles, cambie a la pestaña **Implementaciones**. De forma predeterminada, se muestra una nueva columna que **requiere aprobación**.

#### <a name="bkmk_retry"></a> Reintento de la instalación de aplicaciones aprobadas previamente

<!--4336307-->
A partir de la versión 1906, puede volver a intentar la instalación de una aplicación que haya aprobado previamente para un usuario o dispositivo. La opción de aprobación es solo para las implementaciones disponibles. Si el usuario desinstala la aplicación, o si se produce un error en el proceso de instalación inicial, Configuration Manager no vuelve a evaluar su estado y reinstalarla. Esta característica permite que un técnico de soporte técnico intente volver a instalar la aplicación rápidamente para un usuario que llame para obtener ayuda.

1. Abra la consola de Configuration Manager como un usuario que tenga el permiso **aprobar** en el objeto de aplicación. Por ejemplo, los roles integrados **Administrador de aplicaciones** o **Autor de aplicaciones** tienen este permiso.

1. Implemente una aplicación que requiera aprobación y apruébela.

    > [!Tip]  
    > También puede [instalar una aplicación para un dispositivo](/sccm/apps/deploy-use/install-app-for-device). Crea una solicitud aprobada para la aplicación en el dispositivo.  

Si la aplicación no se instala correctamente o el usuario desinstala la aplicación, use el siguiente proceso para volver a intentarlo:

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Solicitudes de aplicación**. (En la versión 1902 y versiones anteriores, este nodo se denomina **solicitudes de aprobación**).

1. Seleccione la aplicación aprobada previamente. En el grupo Solicitud de aprobación de la cinta, seleccione **Vuelva a intentar la instalación**.

#### <a name="other-app-approval-resources"></a>Otros recursos de aprobación de aplicación

- [Application approval improvements in ConfigMgr 1810](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Application-approval-improvements-in-ConfigMgr-1810/ba-p/303534) (Mejoras de aprobación de aplicaciones en Configuration Manager 1810)
- [Updates to the application approval process in Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/Updates-to-the-application-approval-process-in-Configuration/ba-p/275048) (Actualizaciones del proceso de aprobación de aplicaciones en Configuration Manager)

### <a name="bkmk_prior"></a> Solicitar aprobación del administrador si los usuarios solicitan esta aplicación

> [!Note]  
> Esta experiencia se aplica si no habilita la [experiencia de aprobación de aplicación opcional](#bkmk_opt)recomendada.

El administrador aprueba las solicitudes de usuario sobre la aplicación para que el usuario pueda instalarla. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos.  

Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aplicación**, en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software**. (En la versión 1902 y versiones anteriores, este nodo se denomina **solicitudes de aprobación**). Si una solicitud no se aprueba antes de 30 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  


## <a name="bkmk_email-approve"></a> Notificaciones por correo electrónico

<!--1321550-->

A partir de la versión 1810, configure notificaciones por correo electrónico para las solicitudes de aprobación de aplicaciones. Recibirá un correo electrónico cuando un usuario solicite una aplicación. Haga clic en los vínculos que aparecen en el correo electrónico para aprobar o denegar la solicitud, sin requerir la consola de Configuration Manager.

Puede definir las direcciones de correo electrónico de los usuarios que pueden aprobar o denegar la solicitud durante la creación de una nueva implementación de la aplicación. Si necesita cambiar la lista de direcciones de correo electrónico más adelante, vaya al área de trabajo **Supervisión**, expanda **Alertas** y seleccione el nodo **Suscripciones**. Seleccione **Propiedades** desde una de las suscripciones de **Aprobar aplicación por correo electrónico** que está relacionada con la implementación de la aplicación.

Si hay más de una alerta, puede determinar qué alerta va con cada implementación. Abra las propiedades de alerta y vea la lista de **Alertas seleccionadas** en la pestaña General. La implementación está habilitada como la alerta para esta suscripción.

Los usuarios pueden agregar un comentario a la solicitud desde el Centro de software. Este comentario se muestra en la solicitud de aplicación en la consola de Configuration Manager. A partir de la versión 1902, el comentario también se muestra en el correo electrónico. La inclusión de este comentario en el correo electrónico ayuda a los aprobadores a tomar una decisión más acertada para aprobar o denegar la solicitud.<!--3594063-->


### <a name="prerequisites"></a>Requisitos previos

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Para enviar notificaciones por correo electrónico y realizar acciones en la red interna

Con estos requisitos previos, los destinatarios reciben un correo electrónico con una notificación de la solicitud. Si están en la red interna, también pueden aprobar o denegar la solicitud desde el correo electrónico.

- Habilite la [característica opcional](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Aprobación de solicitudes de aplicación para los usuarios por dispositivo**.  

- Configure la [notificación por correo electrónico para las alertas](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

- Habilitar el proveedor de SMS para usar un certificado.<!--SCCMDocs-pr issue 3135--> Use una de las opciones siguientes:  

    - Habilitar [HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http) (recomendado)  

        > [!Note]  
        > Cuando el sitio crea un certificado para el proveedor de SMS, el explorador web en el cliente no confiará en él. En función de la configuración de seguridad, al responder a una solicitud de aplicación, es posible que vea una advertencia de seguridad.  

    - Enlazar manualmente un certificado basado en PKI al puerto 443 en IIS en el servidor que hospeda el rol de proveedor de SMS  

#### <a name="to-take-action-from-internet"></a>Para realizar acciones desde Internet

Con estos otros requisitos previos opcionales, los destinatarios pueden aprobar o denegar la solicitud desde cualquier lugar con acceso a Internet.

- Habilite el servicio de administración Proveedor de SMS a través de Cloud Management Gateway. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Servidores y roles del sistema de sitios**. Seleccione el servidor con el rol Proveedor de SMS. En el panel de detalles, seleccione el rol **Proveedor de SMS** y luego seleccione **Propiedades** en la cinta, en la pestaña Rol del sitio. Seleccione la opción **Permitir el tráfico de Cloud Management Gateway de Configuration Manager para el servicio de administración**.  

    - El proveedor de SMS requiere **.NET 4.5.2** o posterior.  

- [Puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Incorpore el sitio a los [servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para la **administración en la nube**.  

    - Habilite [Detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).  

    - Configure manualmente las opciones de Azure AD:  

        1. Vaya al [Azure portal](https://portal.azure.com) como usuario con permisos de *administrador global* . Vaya a **Azure Active Directory**y seleccione **registros de aplicaciones**.  

        2. Seleccione la aplicación que creó para la integración de **Administración en la nube** de Configuration Manager.  

        3. En el menú **administrar** , seleccione **autenticación**.  

            1. En la sección **URI de redirección**, pegue la ruta de acceso siguiente: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Reemplace `<CMG FQDN>` por el nombre de dominio completo (FQDN) del servicio Cloud Management Gateway (CMG). Por ejemplo, GraniteFalls.Contoso.com.  

            3. Luego haga clic en **Guardar**.  

        4. En el menú **administrar** , seleccione **manifiesto**.  

            1. En el panel Editar manifiesto, busque la propiedad **oauth2AllowImplicitFlow**.  

            2. Cambie su valor a **true**. Por ejemplo, toda la línea debe ser similar a la siguiente: `"oauth2AllowImplicitFlow": true,`  

            3. Seleccione **Guardar**.  


### <a name="configure-email-approval"></a>Configurar la aprobación por correo electrónico

1. En la consola de Configuration Manager, [implemente una aplicación](/sccm/apps/deploy-use/deploy-applications) como disponible para un grupo de usuarios. En la página **Configuración de implementación**, habilítela para su aprobación. Luego escriba una o varias direcciones de correo electrónico para que reciban la notificación. Separe las direcciones de correo electrónico mediante puntos y coma (`;`).  

     > [!Note]  
     > Cualquier persona de su organización de Azure AD que reciba el correo electrónico puede aprobar la solicitud. No reenvíe el correo electrónico a otros usuarios a menos que quiera que ellos lleven a cabo alguna acción.  

2. Como usuario, solicite la aplicación en Centro de software.  

3. En cinco minutos recibe una notificación por correo electrónico. El contenido del correo electrónico es similar al ejemplo siguiente:  

![Notificación por correo electrónico de ejemplo para la aprobación de aplicación](media/1321550-email.png)

> [!Note]  
> El vínculo para aprobar o denegar es para un solo uso. Por ejemplo, digamos que configura un alias de grupo para recibir notificaciones. Meg aprueba la solicitud. Y ahora, Bruce no puede denegarla.  

Revise el archivo **NotiCtrl.log** en el servidor de sitio para solucionar problemas.


## <a name="maintenance"></a>Mantenimiento

Configuration Manager almacena la información sobre las solicitudes de aprobación de aplicaciones en la base de datos del sitio. En el caso de las solicitudes que se cancelan o se deniegan, el sitio elimina el historial de solicitudes después de 30 días. Se puede configurar este comportamiento de eliminación con la [tarea de mantenimiento del sitio](/sccm/core/servers/manage/maintenance-tasks) **Eliminar datos antiguos de solicitud de la aplicación**. El sitio nunca elimina solicitudes de aplicaciones aprobadas o pendientes.
