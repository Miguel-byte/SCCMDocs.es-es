---
title: Upgrade Readiness
titleSuffix: Configuraton Manager
description: Integre Upgrade Readiness con Configuration Manager. Acceda a datos de compatibilidad de actualización en su consola de administración. Seleccione dispositivos para su actualización o corrección.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 4360fc34e06d4c62c137f8c956274104112d54a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336738"
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Integrar Upgrade Readiness con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Upgrade Readiness (antes Upgrade Analytics) forma parte de [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics), y permite evaluar y analizar si los dispositivos de su entorno están preparados para actualizarse a Windows 10. Puede configurar la versión específica. Upgrade Readiness puede integrarse con Configuration Manager para tener acceso a los datos de compatibilidad de actualización del cliente en la consola de administración de Configuration Manager. Puede seleccionar dispositivos para actualizarse o corregirse mediante recopilaciones dinámicas creadas según estos datos.

Upgrade Readiness es una solución que se ejecuta en [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). Puede leer más información sobre Upgrade Readiness en [Manage Windows upgrades with Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness) (Administración de actualizaciones de Windows con Upgrade Readiness).

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>Configurar clientes

Upgrade Readiness, al igual que todas las soluciones de Windows Analytics, se basa en los datos de telemetría de Windows. Para que Upgrade Readiness reciba suficientes datos de telemetría, deben cumplirse los siguientes requisitos previos:

- Todos los clientes deben estar configurados con una **clave de identificación comercial**. 
- Los clientes de Windows 10 deben tener configurada la telemetría para informar, como mínimo, de datos de telemetría básicos.
-  Los clientes que ejecutan versiones anteriores de Windows deben tener instalado artículos KB específicos tal y como se describe en [Get started with Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs) (Introducción a Upgrade Readiness). También deben tener la telemetría habilitada en **Configuración de cliente**.

La clave de identificación comercial y la telemetría de Windows se pueden configurar en **Configuración de cliente**. Para obtener más información, consulte [Uso de Windows Analytics con Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>Si tiene problemas con Upgrade Readiness porque no recibe los datos de telemetría de los dispositivos del entorno según lo previsto, algunos de estos problemas se pueden solucionar con el [script de implementación de Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-deployment-script). Pero en la mayoría de los entornos que implementan los artículos KB correctos, debería bastar con configurar la telemetría y una clave de identificación comercial en **Configuración del cliente**.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Conexión de Configuration Manager con Upgrade Readiness

A partir de la versión de rama actual 1706, el [Asistente para servicios de Azure](../../../servers/deploy/configure/azure-services-wizard.md) se usa para simplificar el proceso de configuración de servicios de Azure que usa con Configuration Manager. Para conectar Configuration Manager con Upgrade Readiness, se debe crear un registro de aplicación de Azure AD de tipo *aplicación web/API* en [Azure Portal](https://portal.azure.com). Para leer más sobre cómo crear un registro de aplicación, consulte [Registro de una aplicación en un inquilino de Azure Active Directory](/azure/active-directory/active-directory-app-registration). En **Azure Portal**, también debe conceder permisos de *colaborador* a la aplicación web recién registrada en el grupo de recursos que contiene el área de trabajo de OMS que hospeda los datos de Upgrade Readiness. El **Asistente para servicios de Azure** utilizará este registro de aplicación para permitir que Configuration Manager se comunique de manera segura con Azure AD y conecte la infraestructura a los datos de Upgrade Readiness.

>[!IMPORTANT]
>Los permisos de *colaborador* deben conceder permisos a la aplicación en lugar de a una identidad de usuario de Azure AD. Esto es porque se trata de la aplicación registrada y no un usuario de Azure AD que tiene acceso a los datos en nombre de la infraestructura de Configuration Manager. Para conceder los permisos, tendrá que buscar el nombre del registro de aplicación en el área **Agregar usuarios** al asignar el permiso. Es el mismo proceso que se debe seguir al [proporcionar a Configuration Manager permisos para OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) para las conexiones a [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Estos pasos deben realizarse antes de que el registro de aplicación se importe en Configuration Manager con el *Asistente para servicios de Azure*.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Uso del Asistente de Azure para crear la conexión

Siga las instrucciones de [Configuración de servicios de Azure para utilizarlos con Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) para crear una conexión a Upgrade Readiness importando el registro de aplicación web que creó anteriormente. 

En la página *Configuración*, los siguientes valores se rellenan automáticamente si la importación de la aplicación web es correcta y se asignan los permisos correctos en **Azure Portal**. 
-  Suscripciones a Azure
-  Grupo de recursos de Azure
-  Área de trabajo de Windows Analytics

Solo habrá disponible más de un área de trabajo o grupo de recursos si la aplicación web de Azure AD registrada tiene permisos de *colaborador* en más de un grupo de recursos, o bien si el grupo de recursos seleccionado contiene más de un área de trabajo de OMS.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Visualización y uso de la información de Upgrade Readiness en Configuration Manager

Después de integrar Upgrade Readiness con Configuration Manager, puede ver el análisis de la preparación de actualización de los clientes.

1. En la consola de Configuration Manager, pulse **Supervisión** > **Información general** > **Upgrade Readiness**.
2. Revise los datos, que incluyen el estado de preparación de actualización y el porcentaje de dispositivos Windows que están generando informes de telemetría.
3. Puede filtrar el panel para ver los datos de los dispositivos de colecciones determinadas.
4. Puede ver los dispositivos en un estado de preparación determinado y crear una recopilación dinámica para estos, de manera que pueda actualizar estos dispositivos si están listos o tomar medidas para solucionar los que no pueden actualizarse.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Uso del conector de Upgrade Readiness (versión 1702 y anterior)

En la versión 1702 Configuration Manager o anterior, un conjunto diferente de requisitos y pasos son necesarios para crear una conexión a Upgrade Readiness.

### <a name="prerequisites"></a>Requisitos previos

- Para agregar la conexión, el entorno de Configuration Manager debe configurar primero un [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en un [modo en línea](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Al agregar la conexión en el entorno, también se instala Microsoft Monitoring Agent en el equipo que ejecuta este rol de sistema de sitio.
- Registre Configuration Manager como una herramienta de administración de "Aplicación web o API web" y obtenga el [identificador de cliente de este registro](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Cree una clave de cliente para la herramienta de administración registrada en Azure Active Directory.
- En Azure Portal, proporcione la aplicación web registrada con permiso de acceso a OMS, como se describe en [Concesión de permisos a Configuration Manager para acceder a OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Al configurar el permiso para acceder a OMS, asegúrese de elegir el rol **Colaborador** y asignarle permisos al grupo de recursos de la aplicación registrada.

### <a name="create-the-connection"></a>Crear la conexión

1.  En la consola de Configuration Manager, pulse **Administración** > **Cloud Services** > **Upgrade Readiness Connector (Conector de Upgrade Readiness)** > **Create Connection to Upgrade Analytics (Crear conexión para Upgrade Analytics)** para iniciar el **Asistente para agregar una conexión a Upgrade Analytics**.
3.  En la pantalla **Azure Active Directory**, proporcione el **Inquilino**, **Id. de cliente** y **Clave secreta de cliente** y, después, seleccione **Siguiente**.
4.  En la pantalla **Upgrade Readiness**, rellene la **Suscripción de Azure**, el **Grupo de recursos de Azure** y el **Área de trabajo de Operations Management Suite** para proporcionar la configuración de la conexión.
5.  Compruebe la configuración de la conexión en la pantalla **Resumen** y luego seleccione **Siguiente**.

    > [!NOTE]
    > Debe conectar Upgrade Readiness con el sitio de nivel superior de la jerarquía. Si conecta Upgrade Readiness con un sitio primario independiente y después agrega un sitio de administración central al entorno, debe eliminar y volver a crear la conexión de OMS dentro de la nueva jerarquía.
