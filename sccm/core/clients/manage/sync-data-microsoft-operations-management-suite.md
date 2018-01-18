---
title: "Sincronización de datos con Microsoft Operations Management Suite "
titleSuffix: Configuration Manager
description: Sincronice datos de System Center Configuration Manager con Microsoft Operations Management Suite.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: "9"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: bfe500c160bf2ddffd060baabb44cda81337e1cc
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Sincronizar datos de Configuration Manager con Microsoft Operations Management Suite

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede usar el **Asistente para servicios de Azure** para configurar la conexión desde Configuration Manager hasta el servicio en la nube de Operations Management Suite (OMS). A partir de la versión 1706, el asistente reemplaza los flujos de trabajo anteriores para configurar esta conexión. Para las versiones anteriores, consulte [Sincronización de datos de Configuration Manager con Microsoft Operations Management Suite (1702 y versiones anteriores)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   El asistente se usa para configurar los servicios en la nube para Configuration Manager, como OMS, Microsoft Store para Empresas y Azure Active Directory (Azure AD).  

-   Configuration Manager se conecta a OMS para utilizar características como [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) o [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## <a name="prerequisites-for-the-oms-connector"></a>Requisitos previos para el conector de OMS
Los requisitos previos para configurar una conexión a OMS son iguales que los [documentados para la versión 1702 de Rama actual](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Esa información se repite aquí:  

-   Antes de instalar el conector de OMS en Configuration Manager, debe proporcionar permisos de OMS a Configuration Manager. En concreto, debe conceder *acceso de colaborador* al *Grupo de recursos* de Azure que contiene el área de trabajo de Log Analytics de OMS. Los procedimientos para hacerlo se documentan en el contenido de Log Analytics. Vea [Concesión de permisos a Configuration Manager para acceder a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) en la documentación de OMS.

-   El conector de OMS debe instalarse en el equipo que hospeda un [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en [modo en línea](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Debe instalar Microsoft Monitoring Agent para OMS en el punto de conexión de servicio junto con el conector de OMS. El agente y el conector de OMS deben configurarse para usar el mismo **área de trabajo de OMS**. Para instalar el agente, vea [Descarga e instalación del agente](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) en la documentación de OMS.
-   Después de instalar el conector y el agente, debe configurar OMS para utilizar datos de Configuration Manager. Para ello, en el Portal de OMS, vea [Importación de recopilaciones de Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Uso del Asistente para servicios de Azure para configurar la conexión a OMS

1.  En la consola, vaya a **Administración** > **Introducción** > **Cloud Services** > **Servicios de Azure** y, después, elija **Configurar servicios de Azure** en la pestaña **Inicio** de la cinta de opciones para iniciar el **Asistente para servicios de Azure**.

2.  En la página **Servicios de Azure**, seleccione el servicio en la nube de Operation Management Suite. Proporcione un nombre descriptivo para el **Nombre del servicio de Azure** y una descripción opcional y, después, haga clic en **Siguiente**.

3.  En la página **Aplicación**, especifique el entorno de Azure (la versión preliminar técnica admite solo la nube pública). A continuación, haga clic en **Examinar** para abrir la ventana de la aplicación de servidor.

4.  Seleccione una aplicación web:

    -   **Importar**: para usar una aplicación web que ya existe en su suscripción de Azure, haga clic en **Importar**. Proporcione un nombre descriptivo para la aplicación y el inquilino y, después, especifique el identificador del inquilino, el identificador de cliente y la clave secreta de la aplicación web que quiere que use Configuration Manager. Después de **Comprobar** la información, haga clic en **Aceptar** para continuar.   

    > [!NOTE]   
    > Si configura OMS con esta versión preliminar, OMS solo admite la función de *importación* para una aplicación web. No se admite la creación de una nueva aplicación web. Del mismo modo, no se puede reutilizar una aplicación existente para OMS.

5.  Si ha completado todos los demás procedimientos correctamente, aparecerá automáticamente en esta página la información de la pantalla **OMS Connection Configuration** (Configuración de la conexión de OMS). La información para la configuración de la conexión debería aparecer en **Suscripción de Azure**, **Grupo de recursos de Azure** y **Área de trabajo de Operations Management Suite**.

6.  El asistente se conecta al servicio de OMS con la información que ha especificado. Seleccione las recopilaciones de dispositivos que desea sincronizar con OMS y, a continuación, haga clic en **Agregar**.

7.  Compruebe la configuración de la conexión en la pantalla **Resumen** y luego seleccione **Siguiente**. En la pantalla **Progreso** se muestra el estado de la conexión; después debería seleccionar **Completar**.

8.  Cuando finalice el asistente, la consola de Configuration Manager muestra que ha configurado **Operation Management Suite** como un **Tipo de servicio de nube**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Sincronización de datos de Configuration Manager con Microsoft Operations Management Suite (1702 y versiones anteriores)


*Se aplica a: System Center Configuration Manager (1702 y versiones anteriores)*

Puede usar el conector de Microsoft Operations Management Suite (OMS) para sincronizar datos como recopilaciones de System Center Configuration Manager con Log Analytics de OMS en Microsoft Azure. De este modo, los datos de la implementación de Configuration Manager estarán visibles en OMS.
> [!TIP]
> El conector de OMS es una característica de la versión preliminar. Para más información, vea [Uso de las características de versión preliminar de las actualizaciones](/sccm/core/servers/manage/pre-release-features).

A partir de la versión 1702, puede usar el conector de OMS para conectarse a un área de trabajo de OMS que se encuentra en la nube de Microsoft Azure Government. Para ello, puede modificar un archivo de configuración antes de instalar el conector de OMS. Vea [Uso del conector de OMS con la nube de Azure Government](#fairfaxconfig) en este tema.

### <a name="prerequisites"></a>Requisitos previos
- Antes de instalar el conector de OMS en Configuration Manager, debe proporcionar permisos de OMS a Configuration Manager. En concreto, debe conceder *acceso de colaborador* al *Grupo de recursos* de Azure que contiene el área de trabajo de Log Analytics de OMS. Los procedimientos para hacerlo se documentan en el contenido de Log Analytics. Vea [Concesión de permisos a Configuration Manager para acceder a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) en la documentación de OMS.

- El conector de OMS debe instalarse en el equipo que hospeda un [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en [modo en línea](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Si ha conectado OMS a un sitio primario independiente y va a agregar un sitio de administración central a su entorno, debe eliminar la conexión actual y después volver a configurar el conector en el nuevo sitio de administración central.

- Debe instalar Microsoft Monitoring Agent para OMS en el punto de conexión de servicio junto con el conector de OMS.  El agente y el conector de OMS deben configurarse para usar el mismo **área de trabajo de OMS**. Para instalar el agente, vea [Descarga e instalación del agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) en la documentación de OMS.

- Después de instalar el conector y el agente, debe configurar OMS para utilizar datos de Configuration Manager.  Para ello, en el Portal de OMS, vea [Importación de recopilaciones de Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### <a name="install-the-oms-connector"></a>Instalación del conector de OMS  
1. En la consola de Configuration Manager, configure su [jerarquía para usar características de versión preliminar](/sccm/core/servers/manage/pre-release-features) y luego habilite el uso del conector de OMS.  
0
2. Después vaya a **Administración** > **Cloud Services** > **Conector de OMS**. En la cinta, haga clic en "Crear conexión con Operations Management Suite". Se abrirá el **Asistente para conexión a Operations Management Suite**. Seleccione **Siguiente**.  


3.  En la página **General**, confirme que tiene la siguiente información y después seleccione **Siguiente**.  
  - Registró Configuration Manager como una herramienta de administración de "Aplicación web y/o API web" y tiene el [identificador de cliente de este registro](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Creó una clave de cliente para la herramienta de administración registrada en Azure Active Directory.  

  - En el Portal de administración de Azure, proporcionó la aplicación web registrada con permiso de acceso a OMS, como se describe en [Concesión de permisos a Configuration Manager para acceder a OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  En la página **Azure Active Directory**, proporcione el **Inquilino**, **Id. de cliente** y la **Clave secreta de cliente** para configurar la conexión con OMS y después seleccione **Siguiente**.  

5.  En la página **Configuración de conexión de OMS**, rellene la **Suscripción de Azure**, el **Grupo de recursos de Azure** y el **Área de trabajo de Operations Management Suite** para proporcionar la configuración de la conexión.  El área de trabajo debe coincidir con el área de trabajo configurada para el Agente de administración de Microsoft instalado en el punto de conexión de servicio.  

6.  Compruebe la configuración de la conexión en la página **Resumen** y luego seleccione **Siguiente**. En la página **Progreso**, se mostrará el estado de la conexión y después debería seleccionar **Completar**.

Después de haber vinculado Configuration Manager con OMS, puede agregar o quitar recopilaciones y ver las propiedades de la conexión de OMS.

### <a name="verify-the-oms-connector-properties"></a>Verificación de las propiedades del conector de OMS
1.  En la consola de Configuration Manager, vaya a **Administración** > **Cloud Services** y luego seleccione **Conector de OMS** para abrir la página **Conexión a OMS****.
2.  En esta página hay dos pestañas:
  - **Azure Active Directory:**   
    Esta pestaña muestra los valores **Inquilino**, **Id. de cliente** y la **Expiración de la clave secreta de cliente** y le permite verificar si ha expirado la clave secreta de cliente.

  - **Propiedades de conexión a OMS:**  
    Esta pestaña muestra la **Suscripción de Azure**, el **Grupo de recursos de Azure**, el **Área de trabajo de Operations Management Suite** y una lista de **recopilaciones de dispositivos de los que Operations Management Suite puede obtener datos**. Use los botones **Agregar** y **Quitar** para modificar las recopilaciones que se admiten.

### <a name="fairfaxconfig"> </a>Uso del conector de OMS con la nube de Azure Government


1.  En un equipo que tenga instalada la consola de Configuration Manager, edite el archivo de configuración siguiente de modo que apunte a la nube de Government: ***&lt;ruta de acceso de instalación de CM>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Ediciones:**

    Cambie el valor del nombre de la configuración *FairFaxArmResourceID* de modo que sea igual a "https://management.usgovcloudapi.net/"

   - **Original:** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Editado:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Cambie el valor del nombre de la configuración *FairFaxAuthorityResource* de modo que sea igual a "https://login.microsoftonline.us/".

  - **Original:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Editado:** &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.us/&lt;/value>

2.  Después de guardar el archivo con los dos cambios, reinicie la consola de Configuration Manager en el mismo equipo y úsela para instalar el conector de OMS. Para instalar el conector, use la información incluida en [Sincronizar datos de Configuration Manager con Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)y seleccione el **Área de trabajo de Operations Management Suite** que se encuentra en la nube de Microsoft Azure Government.

3.  Cuando se haya instalado el conector de OMS, la conexión a la nube de Government estará disponible al usar cualquier consola que se conecte al sitio.
