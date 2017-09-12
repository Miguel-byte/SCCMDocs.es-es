---
title: Asistente para servicios de Azure | Microsoft Docs
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
ms.openlocfilehash: 3046003f000c8abde28a5b6e3bcb88b159be5357
ms.sourcegitcommit: 2a1328da3facb20b0c78f3b12adbb5fdbe0dcc11
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuración de servicios de Azure para utilizarlos con Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

A partir de la versión de rama actual 1706, el **Asistente para servicios de Azure** se usa para simplificar el proceso de configuración de los servicios de Azure que se emplean con Configuration Manager.

Este asistente ofrece una experiencia de configuración común mediante el uso de una**aplicación web de Azure** para proporcionar los detalles de suscripción y configuración. La aplicación web evita tener que escribir esta misma información cada vez que configura un nuevo servicio o componente de Configuration Manager con Azure.

Los siguientes servicios de Azure se configuran mediante el Asistente para configurar servicios de Azure:
-   **Administración en la nube**   
    [Permita a los clientes autenticarse mediante Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). También puede [configurar la detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **Conector de OMS**
    [Conéctese a Operations Manager Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) y sincronice datos, como colecciones, con Log Analytics de OMS.
-   **Upgrade Readiness**
    [Conéctese a Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) y vea los datos de compatibilidad de actualización de cliente.
-   **Tienda Windows para empresas** Conéctese a la tienda en línea [Tienda Windows para empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) y obtenga aplicaciones para su organización que puede implementar con Configuration Manager.

Al utilizar el asistente para configurar un servicio, hay disponibles varias acciones comunes.
Entre ellos, se incluye:
-   Configurar el entorno de Azure: en la página **Aplicación** página del asistente, seleccione el **entorno de Azure** que desea usar. Vea el contenido de cada servicio para obtener información sobre si admite solo la nube pública de Azure o si también es compatible con una nube privada.
-   Crear o importar una aplicación de servidor: en la página **Aplicación** página del asistente, también puede **crear** e **importar** aplicaciones web de Azure. Las opciones disponibles dependerán del servicio que se va a configurar.  Además, algunos servicios pueden requerir una aplicación adicional. Por ejemplo, un servicio también podría requerir una **aplicación cliente nativa**.


Para obtener más información sobre las aplicaciones web, consulte [Autenticación y autorización en Azure App Service](/azure/app-service/app-service-authentication-overview) e [Introducción a Web Apps](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a> Creación de la aplicación web de Azure para utilizarla Configuration Manager

La aplicación web de servicios de Azure conecta el sitio de Configuration Manager a Azure AD y constituye un requisito previo para usar los servicios de Azure con la infraestructura. Para realizar esta tarea:

1.  En el área de trabajo **Administración** de la consola de Configuration Manager, expanda **Cloud Services** y luego haga clic en **Servicios de Azure**.
2.  En la pestaña **Inicio**, en el grupo **Servicios de Azure**, haga clic en **Configurar servicios de Azure**.
3.  En la página **Servicios de Azure** del Asistente para servicios de Azure, seleccione **Administración en la nube** para permitir que los clientes se autentiquen en la jerarquía mediante Azure AD.
4.  En la página **General** del asistente, especifique un nombre y una descripción para el servicio de Azure.
5.  En la página **Aplicación** del asistente, seleccione su entorno de Azure en la lista y, después, haga clic en **Examinar** para seleccionar la *aplicación web* y la *aplicación cliente nativa* que se usarán para configurar el servicio de Azure.     
    **Aplicación web:** Examinar abre la ventana Aplicación de servidor.    
      En la ventana **Aplicación del servidor**, seleccione la aplicación de servidor que quiera usar y, después, haga clic en **Aceptar**. Las aplicaciones de servidor son las aplicaciones web de Azure que contienen las configuraciones de la cuenta de Azure, incluidos el identificador de inquilino, el identificador de cliente y una clave secreta para los clientes.
    Si no tiene una aplicación de servidor disponible, use una de las siguientes:
        - **Crear**: para crear una nueva aplicación de servidor haga clic en **Crear**. A continuación, escriba un nombre descriptivo para la aplicación, la URL de la página principal, el URI del identificador de aplicación y el período de validez de la clave secreta. De forma predeterminada, el período de validez de la clave secreta es de un año.

         Para continuar, ahora un usuario debe iniciar sesión en Azure para completar el proceso de creación de aplicaciones web en Azure. La cuenta que se utiliza para iniciar sesión en Azure no tiene que ser la misma que ejecuta al Asistente para servicios de Azure. Una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación web en Azure, incluidos el identificador de cliente y la clave secreta que se utilizarán con la aplicación web. Podrá verlos más adelante desde Azure Portal.

         Cuando se utiliza Crear para configurar una aplicación web, Configuration Manager puede crear automáticamente la aplicación web en Azure AD.
        - **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de comprobar la información, haga clic en **Aceptar** para continuar.

          Esta opción no está disponible para todos los servicios que se podrían configurar.

   **Aplicación cliente nativa:** Examinar abre la ventana Aplicación cliente.  
     En la ventana **Aplicación cliente**, seleccione la aplicación cliente que quiera usar y, después, haga clic en **Aceptar**.

     Si no tiene una aplicación cliente disponible, use una de las siguientes:
     - **Crear**: para crear una nueva aplicación de servidor, haga clic en **Crear**. A continuación, proporcione un nombre descriptivo para la aplicación y la dirección URL de respuesta.

          Para continuar, ahora un usuario debe iniciar sesión en Azure para completar el proceso de creación de aplicaciones cliente en Azure. La cuenta que se utiliza para iniciar sesión en Azure no tiene que ser la misma que ejecuta al Asistente para servicios de Azure. Una vez que inicie sesión en Azure, Configuration Manager crea automáticamente la aplicación cliente nativa en Azure, incluidos el identificador de cliente que se utilizará con la aplicación web. Podrá verlos más adelante desde Azure Portal.
          Cuando se utiliza Crear para configurar la aplicación, Configuration Manager puede crear automáticamente la aplicación cliente nativa en Azure AD.
     - **Importar**: para usar una aplicación cliente que ya existe en la suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el identificador de cliente. Luego, haga clic en **Aceptar** para continuar.
           Esta opción no está disponible para todos los servicios que se podrían configurar.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  En la página **Detección** del asistente, haga clic en **Habilitar la detección de usuarios de Azure Active Directory** y, luego, en **Configuración**.
En el cuadro de diálogo **Configuración de detección de usuarios de Azure AD**, configure una programación para cuando se produce la detección. También puede habilitar la detección de diferencias, que busca únicamente las cuentas nuevas o modificadas en Azure AD. Obtenga más información sobre la [detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 7. Complete el asistente.

En este momento, ya ha conectado el sitio de Configuration Manager con Azure AD.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualización de la configuración de un servicio de Azure
Puede ver las propiedades de un servicio de Azure que haya configurado para usarse.

En la consola, vaya a **Administración** > **Introducción** > **Servicios en la nube** > **Servicios de Azure**. Después, elija el servicio que desea ver o editar y, luego, haga clic en **Propiedades**.
