---
title: Requisitos previos de los sitios | Microsoft Docs
description: "Obtenga información sobre los requisitos previos necesarios para instalar los distintos tipos de sitios de System Center Configuration Manager."
ms.custom: na
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: b6c570d8addbe7df5aace461ee725a7df1d35a31
ms.openlocfilehash: 76c8bb6d0922fad996e27c04a86cb9b4ad32a810
ms.lasthandoff: 03/01/2017

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Requisitos previos para instalar sitios de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de iniciar una instalación de sitio, se recomienda obtener información sobre los requisitos previos necesarios para instalar los diferentes tipos de sitios de System Center Configuration Manager.

## <a name="primary-sites-and-the-central-administration-site"></a>Sitios primarios y sitio de administración central
Los siguientes requisitos previos se aplican a la instalación de un sitio de administración central como primer sitio de una jerarquía, a la instalación de un sitio primario independiente o a la instalación de un sitio principal secundario. Si va a instalar un sitio de administración central como parte de una expansión de jerarquía, consulte la sección [Expandir un sitio primario independiente](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) de este tema.

###  <a name="bkmk_PrereqPri"></a> Requisitos previos para instalar un sitio primario o un sitio de administración central  

-   La cuenta de usuario que instale el sitio debe tener los siguientes derechos:  

    -   **Administrador** en el equipo del servidor de sitio  
    -   **Administrador** en todos los equipos que hospedarán la **base de datos del sitio** o una instancia del **proveedor de SMS** del sitio  
    -   **Administrador del sistema** en la instancia de SQL Server que hospeda la base de datos del sitio  

        > [!IMPORTANT]  
        >  Una vez finalizada la instalación, tanto la cuenta de usuario que ejecuta el programa de instalación como la cuenta de equipo del servidor de sitio deben conservar los derechos de administrador del sistema de SQL Server. No quite de estas cuentas los derechos de administrador del sistema.  

-   Si va a instalar un sitio primario, necesita los siguientes derechos adicionales:  
    -  **Administrador** en equipos adicionales en los que vaya a instalar el punto de administración inicial y el punto de distribución, si no se encuentra en el servidor de sitio.  

-   Si va a instalar un nuevo sitio primario secundario debajo de un sitio de administración central, necesita los siguientes derechos adicionales:  

    -   **Administrador** en el equipo que hospeda el sitio de administración central  

    -   Derechos de administración basados en roles en Configuration Manager equivalentes al rol de seguridad de **Administrador de infraestructura** o **Administrador total**.  

-   Debe usar el medio de instalación correcto (archivos de origen) y ejecutar el programa de instalación desde esa ubicación. Para obtener información sobre los archivos de origen correctos para instalar diferentes tipos de sitios, consulte la sección [Opciones para instalar los diferentes tipos de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) del tema [Preparar la instalación de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   El equipo de servidor de sitio debe tener acceso a los archivos de configuración actualizados de Microsoft de una de estas maneras:
    -  Antes de comenzar la instalación, puede descargar y almacenar una copia de estos archivos en la red local usando el [descargador del programa de instalación](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Si no hay disponible ninguna copia local de este archivo, el servidor de sitio debe tener acceso a Internet para descargar estos archivos desde Microsoft durante la instalación.

- Para poder expandir un sitio primario independiente que tenga instalado un rol de sistema de sitio de punto de conexión de servicio, debe desinstalar el punto de conexión de servicio. Se permite solo una instancia de esta función en una jerarquía, y solo en el sitio de nivel superior de la jerarquía. Tendrá la oportunidad de volver a instalar el rol durante la instalación del sitio de administración central.
- El servidor de sitio y los equipos de bases de datos de sitio deben cumplir todos los requisitos previos de configuración. Antes de iniciar el programa de instalación, puede [ejecutar manualmente el Comprobador de requisitos previos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar y corregir problemas.  


### <a name="bkmk_expand"></a> Expandir un sitio primario independiente
Un sitio principal independiente debe cumplir los siguientes requisitos previos antes de que se puede expandir en una jerarquía con un sitio de administración central:

-   **Debe instalar el medio de instalación del nuevo sitio de administración central (que contiene los archivos de origen) que coincida con la versión del sitio primario independiente**

     Para garantizar que las versiones coincidan, instale el sitio nuevo usando los archivos de origen de la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) del sitio primario independiente.

     Para obtener más información sobre los archivos de origen correctos para instalar diferentes sitios, consulte la sección [Opciones para instalar los diferentes tipos de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) del tema [Preparar la instalación de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **No se puede configurar el sitio primario independiente para migrar datos desde otra jerarquía de Configuration Manager**  

     Debe detener la migración activa en el sitio primario independiente de otras jerarquías de Configuration Manager y quitar todas las configuraciones de migración. Esto incluye los trabajos de migración que no han concluido, la recopilación de datos y la configuración de la jerarquía de origen activa.  

     Esto es necesario porque las operaciones de migración las lleva a cabo el sitio de nivel superior de la jerarquía, por lo que las configuraciones para la migración no se transfieren al sitio de administración central cuando se expande un sitio primario independiente.  

     Después de expandir el sitio primario independiente, si se vuelve a configurar la migración en el sitio primario, el sitio de administración central efectuará las operaciones relacionadas con la migración. Para obtener más información sobre cómo configurar la migración, consulte [Configurar jerarquías de origen y sitios de origen para la migración a System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **La cuenta del equipo que hospedará el nuevo sitio de administración central debe ser miembro del grupo de usuarios Administrador del sitio primario independiente**  

     Para expandir correctamente el sitio primario independiente, la cuenta del equipo del nuevo sitio de administración central debe tener derechos de **administrador** en el sitio primario independiente. Esto es necesario únicamente durante la expansión del sitio. La cuenta se puede quitar del grupo de usuarios en el sitio primario cuando haya finalizado la expansión del sitio.  

-   **La cuenta de usuario que ejecuta el programa de instalación para instalar el nuevo sitio de administración central debe tener derechos de administración basados en roles en el sitio primario independiente**  

     Para instalar un sitio de administración central como parte de una expansión de sitios, la cuenta de usuario que ejecuta el programa de instalación para instalar el sitio de administración central debe definirse en la administración basada en roles en el sitio primario independiente como **Administrador total** o **Administrador de infraestructura**.  

-   **Debe desinstalar los siguientes roles de sistema de sitio del sitio primario independiente antes de que pueda expandir el sitio:**  

    -   Punto de sincronización de Asset Intelligence  
    -   Punto de Endpoint Protection  
    -   Punto de conexión de servicio  

   Estos roles de sistema de sitio se admiten únicamente en el sitio de nivel superior de la jerarquía. Por lo tanto, debe desinstalar estos roles de sistema de sitio antes de expandir el sitio primario independiente. Después de expandir el sitio, puede volver a instalar estos roles de sistema de sitio en el sitio de administración central.  

    Todos los demás roles de sistema de sitio pueden permanecer instalados en el sitio primario.  

-   **El puerto de SQL Server Service Broker (SSB) entre el sitio primario independiente y el equipo en el que se instalará el sitio de administración central debe estar abierto**  

     Para replicar correctamente los datos entre un sitio de administración central y un sitio primario, Configuration Manager necesita que haya un puerto abierto entre los dos sitios para que se pueda usar SSB. Al instalar un sitio de administración central y expandir un sitio primario independiente, la comprobación de requisitos previos no comprueba que el puerto especificado para SSB esté abierto en el sitio primario.  


## <a name="bkmk_secondary"></a> Sitios secundarios
A continuación se detallan los requisitos previos para instalar los sitios secundarios:
-   El administrador que configura la instalación del sitio secundario en la consola de Configuration Manager debe tener derechos de administración basada en roles equivalentes al rol de seguridad **Administrador de infraestructura** o **Administrador total**.  
-   La cuenta de equipo del sitio primario principal debe ser un **administrador** en el equipo del servidor de sitio secundario.  
-   Cuando el sitio secundario utiliza una instancia previamente instalada de SQL Server para hospedar la base de datos del sitio secundario:  

    -   La **cuenta de equipo** del sitio primario principal debe tener derechos de **administrador del sistema** en la instancia de SQL Server del equipo de servidor de sitio secundario.  

    -   La cuenta de **sistema local** del equipo de servidor de sitio secundario debe tener derechos de **administrador del sistema** en la instancia de SQL Server del equipo de servidor de sitio secundario.  

        > [!IMPORTANT]  
        >  Una vez finalizada la instalación, las dos cuentas deben conservar los derechos de administrador del sistema de SQL Server. No quite de estas cuentas los derechos de administrador del sistema.  

-   El equipo de servidor de sitio secundario debe cumplir todos los requisitos previos de configuración, incluidos SQL Server y los roles de sistema de sitio predeterminados del punto de administración y el punto de distribución.  

