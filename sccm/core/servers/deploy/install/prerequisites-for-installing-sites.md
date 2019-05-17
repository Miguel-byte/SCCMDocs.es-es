---
title: Requisitos previos de los sitios
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos previos necesarios para instalar los distintos tipos de sitios de Configuration Manager.
ms.date: 04/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2110b805ac404a6e3c12d66225633b45eb50ae
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501357"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Requisitos previos para instalar sitios de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de iniciar una instalación de sitio, obtenga información sobre los requisitos previos necesarios para instalar los diferentes tipos de sitios de Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Sitios primarios y sitio de administración central

Estos son los requisitos previos para instalar uno de los tipos siguientes:
- Un sitio de administración central como primer sitio de una jerarquía
- Un sitio primario independiente
- Un sitio primario secundario

Si va a instalar un sitio de administración central como parte de una expansión de jerarquía, consulte la sección [Expandir un sitio primario independiente](#bkmk_expand).


###  <a name="bkmk_PrereqPri"></a> Requisitos previos para instalar un sitio primario o un sitio de administración central  

- Deben instalarse los siguientes roles de Windows Server, características y componentes de Windows:  
    - .NET framework 3.5 SP1 (o posterior)
    - .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2
    - Compresión diferencial remota
    - Windows ADK
    - Visual C++ Redistributable  
    
    Para obtener más información, consulte [Requisitos previos de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012sspreq)  

- La cuenta de usuario que instale el sitio debe tener los siguientes derechos:  

    - **Administrador** en los siguientes servidores:  
        - El servidor de sitio  
        - Cada servidor que hospeda la **base de datos del sitio**  
        - Cada instancia del **Proveedor de SMS** para el sitio  

    - **Administrador del sistema** en la instancia de SQL Server que hospeda la base de datos del sitio  

        > [!IMPORTANT]  
        >  Una vez finalizada la instalación de Configuration Manager, tanto la cuenta de usuario que ejecuta el programa de instalación como la cuenta de equipo del servidor de sitio deben conservar los derechos de administrador del sistema de SQL Server. No quite de estas cuentas los derechos de administrador del sistema.  

- Si va a instalar un sitio primario, necesita los siguientes derechos adicionales:  

    - **Administrador** en servidores adicionales en los que vaya a instalar el punto de administración inicial y el punto de distribución, si no se encuentra en el servidor de sitio  

- Si va a instalar un nuevo sitio primario secundario debajo de un sitio de administración central, necesita los siguientes derechos adicionales:  

    - **Administrador** en el servidor que hospeda el sitio de administración central  

    - Derechos de administración basados en roles en Configuration Manager equivalentes al rol de seguridad de **Administrador de infraestructura** o **Administrador total**.  

- Use los archivos de origen de instalación correctos y ejecute el programa de instalación desde esa ubicación. Para obtener información sobre los archivos de origen correctos para instalar diferentes tipos de sitios, consulte [Opciones para instalar los diferentes tipos de sitios](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

- El servidor de sitio debe tener acceso a los archivos de configuración actualizados de Microsoft de una de estas maneras:  

    - Antes de comenzar la instalación, descargue y almacene una copia de estos archivos en la red local. Para obtener más información, consulte [Descargador del programa de instalación](/sccm/core/servers/deploy/install/setup-downloader).  

    - Si no hay disponible una copia local de estos archivos, el servidor de sitio debe tener acceso a Internet. Descarga estos archivos de Microsoft durante la instalación.  

- El servidor de sitio y el servidor de bases de datos de sitio deben cumplir todos los requisitos previos de configuración. Antes de iniciar el programa de instalación de Configuration Manager, [ejecute manualmente el Comprobador de requisitos previos](/sccm/core/servers/deploy/install/prerequisite-checker) para identificar y corregir problemas.  


### <a name="bkmk_expand"></a> Requisitos previos para expandir un sitio primario independiente

Un sitio principal independiente debe cumplir los siguientes requisitos previos antes de que se puede expandir en una jerarquía con un sitio de administración central:

#### <a name="source-file-version-matches-site-version"></a>La versión del archivo de origen coincide con la versión del sitio
Instale el nuevo sitio de administración central con el medio de una carpeta CD.Latest que coincida con la versión del sitio primario independiente. Para garantizar que las versiones coincidan, use los archivos de origen que se encuentran en la [carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) del sitio primario independiente. 

Para obtener más información sobre los archivos de origen correctos para instalar diferentes sitios, consulte [Opciones para instalar los diferentes tipos de sitios](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Detención de la migración activa desde otra jerarquía
No puede configurar el sitio primario independiente para migrar datos desde otra jerarquía de Configuration Manager. Detenga la migración activa en el sitio primario independiente de otras jerarquías de Configuration Manager y quitar todas las configuraciones de migración. Estas configuraciones incluyen: 
- Trabajos de migración que no se han completado  
- Recopilación de datos  
- La configuración de la jerarquía de origen activo  

Esta configuración es necesaria porque Configuration Manager migra los datos desde el sitio de nivel superior de la jerarquía. Al expandir un sitio primario independiente, las configuraciones para la migración no se transfieren al sitio de administración central.  

Después de expandir el sitio primario independiente, si se vuelve a configurar la migración en el sitio primario, el sitio de administración central efectuará las operaciones de migración. 

Para obtener más información sobre cómo configurar la migración, consulte [Configurar jerarquías de origen y sitios de origen para la migración](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration).  

#### <a name="computer-account-as-administrator"></a>Cuenta de equipo como administrador
La cuenta del equipo del servidor que hospeda el nuevo sitio de administración central debe ser miembro del grupo **Administradores** del servidor del sitio primario independiente. 

Para expandir correctamente el sitio primario independiente, la cuenta del equipo del nuevo sitio de administración central debe tener derechos de **administrador** en el sitio primario independiente. Esto es necesario únicamente durante la expansión del sitio. Cuando finalice la expansión del sitio, puede quitar la cuenta del grupo de usuarios en el sitio principal.  

#### <a name="installation-account-permissions"></a>Permisos de la cuenta de instalación
La cuenta de usuario que ejecuta el programa de instalación de Configuration Manager para instalar el nuevo sitio de administración central debe tener derechos de administración basados en roles en el sitio primario independiente.

Para instalar un sitio de administración central como parte de una expansión de sitios, la cuenta de usuario que ejecuta el programa de instalación para instalar el sitio de administración central debe definirse en la administración basada en roles en el sitio primario independiente como **Administrador total** o **Administrador de infraestructura**.  

#### <a name="top-level-site-roles"></a>Roles del sitio de nivel superior
Antes de expandir el sitio, desinstale los siguientes roles de sistema de sitio del sitio primario independiente:

- Punto de sincronización de Asset Intelligence  
- Punto de Endpoint Protection  
- Punto de conexión de servicio  

Configuration Manager solo admite estos roles en el sitio de nivel superior de la jerarquía. Desinstale estos roles de sistema de sitio antes de expandir el sitio primario independiente. Después de expandir el sitio, vuelva a instalar estos roles de sistema de sitio en el sitio de administración central.  

Todos los demás roles de sistema de sitio pueden permanecer instalados en el sitio primario.  

#### <a name="open-the-sql-server-service-broker-port"></a>Abra el puerto de SQL Server Service Broker
El puerto de red debe estar abierto para SQL Server Service Broker (SBB) entre el sitio primario independiente y el servidor del sitio de administración central.  

Para replicar correctamente los datos entre un sitio de administración central y un sitio primario, Configuration Manager necesita que haya un puerto abierto entre los dos sitios para que se pueda usar SSB. Al instalar un sitio de administración central y expandir un sitio primario independiente, la comprobación de requisitos previos no verifica que el puerto especificado para SSB esté abierto en el sitio primario.  

#### <a name="known-issues-with-azure-services"></a>Problemas conocidos con servicios de Azure
Si usa uno de los siguientes servicios de Azure con Configuration Manager, deberá eliminar y volver a crear la conexión al servicio después de la ampliación del sitio.

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [Preparación para la actualización](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [Microsoft Store para Empresas](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

Para resolver el problema, siga estos pasos:
 1. En la consola de Configuration Manager, elimine el servicio de Azure desde el nodo de **servicios de Azure**.  

 2. En Azure Portal, elimine el inquilino que está asociado al servicio desde el nodo de inquilinos de Azure Active Directory. Esto también elimina la aplicación web de Azure AD asociada al servicio.  

 3. Vuelva a configurar la conexión al servicio de Azure para su uso con Configuration Manager.  



## <a name="bkmk_secondary"></a> Sitios secundarios

A continuación se detallan los requisitos previos para instalar los sitios secundarios:  

- Deben instalarse los siguientes roles de Windows Server, características y componentes de Windows:  
    - .NET framework 3.5 SP1 (o posterior)
    - .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 o 4.7.2
    - Compresión diferencial remota
    - Visual C++ Redistributable  
    
    Para obtener más información, consulte [Requisitos previos de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012secpreq)  

- El administrador que configura la instalación del sitio secundario en la consola de Configuration Manager debe tener derechos de administración basada en roles equivalentes al rol de seguridad **Administrador de infraestructura** o **Administrador total**.  

- La cuenta de equipo del sitio primario principal debe ser un **administrador** en el servidor de sitio secundario.  

- Cuando el sitio secundario utiliza una instancia previamente instalada de SQL Server para hospedar la base de datos del sitio secundario:  

    - La **cuenta de equipo** del sitio primario principal debe tener derechos de administrador del sistema en la instancia de SQL Server del servidor de sitio secundario.  

    - La cuenta de **sistema local** del equipo de servidor de sitio secundario debe tener derechos de **administrador del sistema** en la instancia de SQL Server del servidor de sitio secundario.  

        > [!IMPORTANT]  
        >  Una vez finalizada la instalación de Configuration Manager, las dos cuentas deben conservar los derechos de administrador del sistema de SQL Server. No quite de estas cuentas los derechos de administrador del sistema.  

- El servidor de sitio secundario debe cumplir todos los requisitos previos de configuración. Estas configuraciones incluyen SQL Server y los roles de sistema de sitio predeterminados del punto de administración y el punto de distribución.  
