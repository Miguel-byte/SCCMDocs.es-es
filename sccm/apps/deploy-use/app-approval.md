---
title: Aprobar aplicaciones
titleSuffix: Configuration Manager
description: Obtenga información sobre la configuración y los comportamientos de la aprobación de aplicaciones en Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1352669db30ad2fad1d7287998227ce1556274d
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403376"
---
# <a name="approve-applications-in-configuration-manager"></a>Aprobar aplicaciones en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Al [implementar una aplicación](/sccm/apps/deploy-use/deploy-applications) en Configuration Manager, se puede necesitar su aprobación antes de instalarla. Los usuarios solicitan la aplicación en el Centro de software y la solicitud se revisa en la consola de Configuration Manager. La solicitud se puede aprobar o denegar.


## <a name="bkmk_approval"></a> Configuración de aprobación

El comportamiento de aprobación de una aplicación depende de la versión de Configuration Manager. En la página **Configuración de implementación** de la implementación de aplicaciones aparece una de las siguientes opciones de aprobación:  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>Solicitar aprobación del administrador si los usuarios solicitan esta aplicación

*Se aplica a las versiones 1710 y anteriores*

El administrador aprueba las solicitudes de usuario sobre la aplicación para que el usuario pueda instalarla. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos.  

Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aprobación** , en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** . Si una solicitud no se aprueba antes de 30 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  

#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo

*Se aplica a las versiones 1802 y posteriores <sup>[Nota 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **Nota 1**: Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).
>
> Si no habilita esta característica, verá la experiencia anterior.  

El administrador aprueba las solicitudes de usuario sobre la aplicación para que el usuario pueda instalarla en el dispositivo solicitado. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos. <!--1357015-->  

> [!Note]  
> Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.<!--SCCMDocs issue 646-->  

Vea **Solicitudes de aprobación** en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** de la consola de Configuration Manager. Hay una columna **Dispositivo** en la lista de cada solicitud. Al realizar acciones en la solicitud, el cuadro de diálogo Solicitud de aplicación también incluye el nombre del dispositivo desde el que el usuario envió la solicitud.  

Si una solicitud no se aprueba antes de 30 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  

> [!Important]  
> A partir de la versión 1806, *el comportamiento ha cambiado* al revocar la aprobación de una aplicación que se haya aprobado e instalado anteriormente. Ahora, al **Denegar** la solicitud de la aplicación, el cliente desinstala la aplicación del dispositivo del usuario.<!--1357891-->  

Automatice el proceso de aprobación con el cmdlet [Approve-CMApprovalRequest](https://docs.microsoft.com/powershell/module/configurationmanager/approve-cmapprovalrequest?view=sccm-ps) de PowerShell. A partir de la versión 1902, este cmdlet incluye el parámetro **InstallActionBehavior**. Use este parámetro para especificar si quiere instalar la aplicación de inmediato o fuera del horario laboral.<!-- SCCMDocs-pr issue #3418 -->


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

        1. Vaya a [Azure Portal](https://portal.azure.com), seleccione **Azure Active Directory** y luego **Registros de aplicaciones**.  

        2. Seleccione la aplicación de tipo **Nativo** que ha creado para la integración de **Administración en la nube** de Configuration Manager.  

        3. En las propiedades de la aplicación, seleccione **Configuración** y luego **URI de redirección**.  

            1. En el panel URI de redirección, pegue la ruta de acceso siguiente: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Reemplace `<CMG FQDN>` por el nombre de dominio completo (FQDN) del servicio Cloud Management Gateway (CMG). Por ejemplo, GraniteFalls.Contoso.com.  

            3. Luego haga clic en **Guardar**. Cierre el panel **Configuración**.  

        4. En las propiedades de la aplicación, seleccione **Manifiesto**.  

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
