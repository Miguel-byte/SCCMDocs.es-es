---
title: Sincronización de datos en Log Analytics
titleSuffix: Configuration Manager
description: Sincronice datos de Configuration Manager a Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b3ba4c5179069e5443beaf1b7f733c797cfd680
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156532"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Sincronización de datos de Configuration Manager a Azure Log Analytics

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1258052--> Use el **Asistente para servicios de Azure** para configurar una conexión desde Configuration Manager al servicio en la nube de Azure Log Analytics. Esta conexión sincroniza los datos de la recopilación de dispositivos a Log Analytics. 

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para más información, vea [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> A partir de Configuration Manager 1802, el conector de Log Analytics ya no es una característica de versión preliminar. Para más información, vea [Uso de las características de versión preliminar de las actualizaciones](/sccm/core/servers/manage/pre-release-features).



## <a name="prerequisites-for-the-log-analytics-connector"></a>Requisitos previos para el conector de Log Analytics

> [!Note]  
> Este artículo se refiere al *conector de Log Analytics*, que anteriormente se denominaba *conector de OMS*. No hay ninguna diferencia funcional. Para obtener más información, vea [Administración de Azure: supervisión](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Antes de instalar el conector de Log Analytics en Configuration Manager, proporcione permisos a Configuration Manager. Conceda *acceso de colaborador* al *grupo de recursos* de Azure que contiene el área de trabajo de Log Analytics. Para obtener más información, vea [Concesión de permisos a Configuration Manager para acceder a Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Instale el conector de Log Analytics en el equipo que hospeda el [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en modo en línea.  

- Instale Microsoft Monitoring Agent para Log Analytics en el punto de conexión de servicio junto con el conector. Configure este agente y el conector para que usen la misma área de trabajo de Log Analytics. Para obtener más información acerca de cómo instalar este agente, consulte [Descarga e instalación del agente](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- Después de instalar el conector y el agente, configure Log Analytics para utilizar datos de Configuration Manager. Para obtener más información, vea [Importación de recopilaciones](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## <a name="configure-the-connection-to-log-analytics"></a>Configuración de la conexión a Log Analytics

Use el **Asistente para servicios de Azure** para configurar una conexión desde Configuration Manager al servicio en la nube de Azure Log Analytics. Para obtener más información y detalles de este proceso, vea [Configuración de servicios de Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Seleccione la opción en el Asistente para el **conector de OMS**. 

> [!Note]  
> Este artículo se refiere al *conector de Log Analytics*, que anteriormente se denominaba *conector de OMS*. No hay ninguna diferencia funcional. Para obtener más información, vea [Administración de Azure: supervisión](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

Si ha completado todos los demás procedimientos correctamente, la información sobre la pantalla **Configuración de conexión** aparece automáticamente tras importar la aplicación web. La información para la configuración de la conexión debería aparecer en **Suscripción de Azure**, **Grupo de recursos de Azure** y **Área de trabajo de Operations Management Suite**.

El asistente se conecta al servicio de Log Analytics con la información que ha especificado. Seleccione las recopilaciones de dispositivos que desea sincronizar con el servicio en la nube y, a continuación, haga clic en **Agregar**.


## <a name="verify-the-connector-properties"></a>Verificación de las propiedades del conector

Después de vincular Configuration Manager con Log Analytics, vea las propiedades de la conexión para agregar o quitar recopilaciones. 

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**.  

2. Seleccione la conexión de Log Analytics. En la cinta, seleccione **Propiedades**.  

La página de propiedades tiene las siguientes dos pestañas:  

#### <a name="azure-active-directory"></a>Azure Active Directory
Esta pestaña muestra los atributos siguientes: 
- **Inquilino**  
- **Id. de cliente**  
- **Expiración de la clave secreta de cliente**  

Verifique también cuándo expira la clave del secreto de cliente.

#### <a name="connection-properties"></a>Propiedades de la conexión
Esta pestaña muestra los atributos siguientes: 
- **Suscripción de Azure**  
- **Grupo de recursos de Azure**  
- **Área de trabajo de Log Analytics**  

También muestra la lista de **recopilaciones de dispositivos**. Use los botones **Agregar** y **Quitar** para modificar las recopilaciones que se sincronizarán.
