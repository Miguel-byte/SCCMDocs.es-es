---
title: Asistente para servicios de Azure
titleSuffix: Configuration Manager
description: "Este artículo trata sobre el Asistente para servicios de Azure de System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 833bc6588e079e124209d9c7adb91062e6afe6c3
ms.sourcegitcommit: d025a2cbd1ed82f42f67255c97b913f2163b3baf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuración de servicios de Azure para utilizarlos con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

A partir de la versión de rama actual 1706, el **Asistente para servicios de Azure** se usa para simplificar el proceso de configuración los servicios de Azure que se usan con Configuration Manager.

Este asistente proporciona una experiencia de configuración común en la que se usa un **registro de aplicación web de Azure AD** para proporcionar los detalles de suscripción y configuración y autenticar las comunicaciones con Azure AD. La aplicación web evita tener que escribir esta misma información cada vez que configura un nuevo servicio o componente de Configuration Manager con Azure.

Los siguientes servicios de Azure se pueden configurar mediante el Asistente para servicios de Azure:
-   **Administración en la nube**   
    [Permita a los clientes autenticarse mediante Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). También puede [configurar la detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Conector de OMS**
    [Conéctese a Operations Management Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) y sincronice datos, como colecciones, con Log Analytics de OMS.
-   **Upgrade Readiness**
    [Conéctese a Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) y vea los datos de compatibilidad de actualización de cliente.
-   **Microsoft Store para Empresas** Conéctese a [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) y obtenga aplicaciones para su organización que puede implementar con Configuration Manager.

Al utilizar el asistente para configurar un servicio, hay disponibles varias acciones comunes.
Entre ellos, se incluye:
-   *Configurar el entorno de Azure*: en la página **Aplicación** del asistente, seleccione el **entorno de Azure** que quiere usar. Vea el contenido de cada servicio para obtener información sobre si admite solo la nube pública de Azure o si también es compatible con una nube privada.
-   *Crear o importar una aplicación de servidor*: en la página **Aplicación** del asistente, también puede **crear** e **importar** metadatos del registro de aplicación web de Azure. Las opciones disponibles dependen del servicio que se va a configurar. Además, algunos servicios pueden requerir una aplicación adicional. Por ejemplo, el servicio **Cloud Management** requiere una **aplicación cliente nativa** que se usa para que los clientes autentiquen directamente las comunicaciones con servicios de Azure.


Para más información sobre las aplicaciones web, consulte [Autenticación y autorización en Azure App Service](/azure/app-service/app-service-authentication-overview) e [Introducción a Web Apps](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a> Creación o importación de un registro de aplicación web de Azure Active Directory para su uso con Configuration Manager

El registro de aplicación web de servicios de Azure conecta el sitio de Configuration Manager a Azure AD y constituye un requisito previo para usar los servicios de Azure con la infraestructura. Para realizar esta tarea:

1.  En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services** y luego haga clic en **Servicios de Azure**.
2.  En la pestaña **Inicio**, en el grupo **Servicios de Azure**, haga clic en **Configurar servicios de Azure**.
3.  En la página **Servicios de Azure** del Asistente para servicios de Azure, seleccione el servicio de Azure que quiere conectar a Configuration Manager.
4.  En la página **General** del asistente, especifique un nombre y una descripción para el servicio de Azure.
5.  En la página **Aplicación** del asistente, seleccione su entorno de Azure en la lista y, después, haga clic en **Examinar** para seleccionar la *aplicación web* y la *aplicación cliente nativa* (solo si es necesario) que se usarán para configurar el servicio de Azure.

    **Aplicación web:** Examinar abre la ventana Aplicación de servidor.    
      En la ventana **Aplicación del servidor**, seleccione la aplicación de servidor que quiera usar y, después, haga clic en **Aceptar**. Las aplicaciones de servidor son los registros de aplicaciones web de Azure AD que contienen las configuraciones de la cuenta de Azure, incluidos el identificador de inquilino, el identificador de cliente y una clave secreta para los clientes.
    Si no tiene una aplicación de servidor disponible, use una de las siguientes:

    - **Crear**: automatice la creación de un registro de aplicación web de Azure AD según la información insertada en la consola de Configuration Manager. Proporcione un nombre descriptivo para la aplicación, la URL de la página principal, el URI del identificador de aplicación y el período de validez de la clave secreta. De forma predeterminada, el período de validez de la clave secreta es de un año.
        
        Para continuar, alguien debe ahora iniciar sesión con sus credenciales de Azure AD para completar la creación de aplicaciones web en Azure. La cuenta que se utiliza para iniciar sesión en Azure no tiene que ser la misma que ejecuta al Asistente para servicios de Azure. Una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación web en Azure, incluidos el identificador de cliente y la clave secreta que se usarán con la aplicación web. Podrá verlos más adelante desde Azure Portal.

        Cuando se utiliza *Crear* para configurar una aplicación web, Configuration Manager puede crear automáticamente la aplicación web en Azure AD.
    
    - **Importar**: escriba información sobre un registro de aplicación web de Azure AD que ya se ha creado en **Azure Portal** para importar metadatos sobre ese registro en Configuration Manager. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de comprobar la información, haga clic en **Aceptar** para continuar.
        > [!NOTE]
        > Para que pueda usarse la **importación**, se debe crear un registro de aplicación de Azure AD de tipo *aplicación web/API* en [Azure Portal](https://portal.azure.com). Para leer más sobre cómo crear un registro de aplicación, consulte [Registro de una aplicación en un inquilino de Azure Active Directory](/azure/active-directory/active-directory-app-registration). Al configurar Upgrade Readiness o Operations Management Suite, también deberá proporcionar los permisos de *colaborador* de la aplicación web recién registrada en el grupo de recursos que contiene el área de trabajo de OMS pertinente para que Configuration Manager pueda acceder a ella. Para ello, tendrá que buscar el nombre del registro de aplicación en la hoja **Agregar usuarios** al asignar el permiso. Este es el mismo proceso que se debe seguir al [proporcionar a Configuration Manager permisos a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) para las conexiones a [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Antes de que la aplicación se importe en Configuration Manager, se deben asignar estos permisos.


    **Aplicación cliente nativa:** Examinar abre la ventana Aplicación cliente.  
     En la ventana **Aplicación cliente**, seleccione la aplicación cliente que quiera usar y, después, haga clic en **Aceptar**.

     Si no tiene una aplicación cliente disponible, use una de las siguientes:
     - **Crear**: para crear una nueva aplicación de servidor, haga clic en **Crear**. A continuación, proporcione un nombre descriptivo para la aplicación y el identificador URI de redirección.

         Para continuar, alguien debe ahora iniciar sesión con sus credenciales de Azure AD para completar la creación de aplicaciones web en Azure. La cuenta que se utiliza para iniciar sesión en Azure no tiene que ser la misma que ejecuta al Asistente para servicios de Azure. Después de iniciar sesión en Azure, Configuration Manager crea automáticamente la aplicación cliente nativa en Azure, lo que incluye el identificador de cliente y la clave secreta. Podrá verlos más adelante desde [Azure Portal](https://portal.azure.com). 

     - **Importar**:use una aplicación cliente que ya exista en la suscripción de Azure. Proporcione un nombre descriptivo para la aplicación y el identificador de cliente. Luego, haga clic en **Aceptar** para continuar.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  (Solo al configurar el servicio **Cloud Management**) En la página **Detección** del asistente, haga clic en **Habilitar la detección de usuarios de Azure Active Directory** y luego haga clic en **Configuración**.
En el cuadro de diálogo **Configuración de detección de usuarios de Azure AD**, configure una programación para cuando se produce la detección. También puede habilitar la detección de diferencias, que busca únicamente las cuentas nuevas o modificadas en Azure AD. Obtenga más información sobre la [detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

7.  Complete el asistente.

En este momento, ha completado la configuración de un servicio de Azure en Configuration Manager. Puede repetir este proceso para configurar otros servicios de Azure.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualización de la configuración de un servicio de Azure
Puede ver las propiedades de un servicio de Azure que haya configurado para usarse.

En la consola, vaya a **Administración** > **Introducción** > **Servicios en la nube** > **Servicios de Azure**. Después, elija el servicio que desea ver o editar y, luego, haga clic en **Propiedades**.
