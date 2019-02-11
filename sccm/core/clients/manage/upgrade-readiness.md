---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Integre Upgrade Readiness con Configuration Manager para tener acceso a datos de compatibilidad de la actualización a Windows 10 y los dispositivos de destino para su actualización o corrección.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 0ba5a484fe11185b46125de0d8764bce153f577d
ms.sourcegitcommit: a2ecd84d93f431ee77848134386fec14031aed6a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2019
ms.locfileid: "55230858"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Integración de Upgrade Readiness con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Upgrade Readiness forma parte de [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). Le permite evaluar y analizar si los dispositivos del entorno están preparados para actualizarse a Windows 10. Integre Upgrade Readiness con Configuration Manager para tener acceso a los datos de compatibilidad de actualización del cliente en la consola de Configuration Manager. Use luego estos datos para crear recopilaciones, y los dispositivos para su actualización o corrección.



## <a name="configure-clients"></a>Configurar clientes

Upgrade Readiness se basa en datos de Windows Analytics. Para que Upgrade Readiness reciba suficientes datos, configure los siguientes requisitos previos:

- Configure todos los clientes con una *clave de identificación comercial*  

- Configure los clientes de Windows 10 para Windows Analytics para que notifiquen al menos los datos de nivel básico  

- Para los clientes que ejecutan Windows 7 o 8.1:  

    - Instale las actualizaciones como se describe en [Get started with Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs) (Introducción a Upgrade Readiness)  

    - Habilitación de los ajustes de cliente de Windows Analytics  

Configure estos valores mediante los ajustes del cliente de Configuration Manager. Para obtener más información, consulte [Uso de Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> La implementación de las actualizaciones de requisitos previos correctas y la configuración de los ajustes de cliente debería ser suficiente en la mayoría de entornos. Si tiene problemas con Upgrade Readiness porque no recibe los datos de los dispositivos del entorno, algunos de estos problemas se pueden solucionar con el [script de implementación de Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Conexión de Configuration Manager con Upgrade Readiness

Use el [Asistente para servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para simplificar el proceso de configuración de los servicios de Azure que se usan con Configuration Manager. Para conectar Configuration Manager con Upgrade Readiness, cree un registro de aplicación de Azure Active Directory (Azure AD) de tipo *aplicación web/API* en [Azure Portal](https://portal.azure.com). Para leer más sobre cómo crear un registro de aplicación, consulte [Register your application with your Azure AD tenant](/azure/active-directory/active-directory-app-registration) (Registro de la aplicación con su inquilino de Azure AD). 

En Azure Portal, asigne los siguientes permisos a la aplicación web recién registrada:
- Permisos de *lector* en el grupo de recursos que contiene el área de trabajo de Log Analytics con los datos de Upgrade Readiness
- Permisos de *colaborador* para el área de trabajo de Log Analytics que hospeda los datos de Upgrade Readiness

El Asistente para servicios de Azure utiliza este registro de aplicación para permitir que Configuration Manager se comunique de manera segura con Azure AD y conecte la infraestructura a los datos de Upgrade Readiness.

> [!IMPORTANT]  
> Conceda permisos a la propia aplicación, no a una identidad de usuario de Azure AD. Se trata de la aplicación registrada que tiene acceso a los datos en nombre de la infraestructura de Configuration Manager. Para conceder los permisos, busque el nombre del registro de aplicación en el área **Agregar usuarios** al asignar el permiso. 
> 
> Este proceso es el mismo que la concesión de permisos a Configuration Manager para acceder a Log Analytics. Estos pasos deben realizarse antes de que el registro de aplicación se importe en Configuration Manager con el *Asistente para servicios de Azure*.
> 
> Para obtener más información, consulte [Conexión de Configuration Manager con Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Uso del Asistente de Azure para crear la conexión

Siga las instrucciones de [Configuración de servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) para crear una conexión a Upgrade Readiness importando el registro de aplicación web que creó anteriormente. 

Si la importación de la aplicación web se completó correctamente y se asignaron los permisos adecuados en Azure Portal, la página *Configuración* se rellena automáticamente con los valores siguientes:   
-  Suscripciones a Azure  
-  Grupo de recursos de Azure  
-  Área de trabajo de Windows Analytics  

Más de un área de trabajo o grupo de recursos está disponible en las siguientes circunstancias: 
- Si la aplicación web de Azure AD registrada tiene permisos de *colaborador* en más de un grupo de recursos   
- Si el grupo de recursos seleccionado tiene más de un área de trabajo de Log Analytics  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Visualización y uso de la información de Upgrade Readiness en Configuration Manager

Después de integrar Upgrade Readiness con Configuration Manager, puede ver el análisis de la preparación de actualización de los clientes.

1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Upgrade Readiness**.  

2. Revise los datos. Por ejemplo:  
    - Estado de Upgrade Readiness  
    - El porcentaje de dispositivos de Windows que notifican datos  

3. Filtre el panel para ver los datos de los dispositivos de recopilaciones determinadas.  

4. Vea los dispositivos en un estado de preparación determinado y, a continuación, cree una recopilación dinámica para esos dispositivos. Luego use esa recopilación para actualizar estos dispositivos, o tome medidas para corregir los dispositivos que están en un estado bloqueado.  

> [!Note]  
> El sitio sincroniza los datos con Upgrade Readiness una vez por semana.<!--SCCMDocs issue 732--> Para desencadenar manualmente la sincronización:
> 1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**.  
> 2. Seleccione la conexión a Upgrade Readiness en la lista.  
> 3. En la cinta de opciones, seleccione la opción para sincronizar.  



## <a name="next-steps"></a>Pasos siguientes

- [Actualizar Windows a la versión más reciente](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Creación de una secuencia de tareas para actualizar un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Crear implementaciones por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
