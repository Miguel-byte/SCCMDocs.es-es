---
title: Requisitos previos de los sitios | System Center Configuration Manager
description: "Obtenga información sobre los diferentes requisitos previos necesarios para instalar los distintos tipos de sitios de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bf3b1e4d87a972f530590bf94e38a5ec66c4fc9a

---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Requisitos previos para instalar sitios de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


En las siguientes secciones se proporciona información detallada sobre los diferentes requisitos previos necesarios para instalar los distintos tipos de sitios de System Center Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Sitios primarios y sitio de administración central
Los siguientes requisitos previos se aplican a la instalación de un sitio de administración central como primer sitio de una jerarquía, un sitio primario independiente o un sitio principal secundario. Si va a instalar un sitio de administración central como parte de un escenario de expansión de jerarquía, consulte la sección [Expandir un sitio primario independiente](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand
) de este tema.

####  <a name="a-namebkmkprereqpria-prerequisites-to-install-a-primary-site-or-central-administration-site"></a><a name="bkmk_PrereqPri"></a> Requisitos previos para instalar un sitio primario o un sitio de administración central  

-   El usuario que vaya a instalar el sitio debe tener los permisos siguientes:  

    -   **Administrador local** en el equipo del servidor de sitio  

    -   **Administrador local** en cada equipo que hospedará el **sitio de la base de datos** , o bien una instancia del parámetro **SMS_Provider** del sitio  

    -   **Administrador del sistema** en la instancia de SQL Server que hospeda la base de datos del sitio  

        > [!IMPORTANT]  
        >  Una vez completada la instalación, tanto la cuenta de usuario que ejecuta el programa de instalación como la cuenta de equipo del servidor de sitio deben conservar los derechos de administrador del sistema de SQL Server. Los derechos de administrador del sistema no se pueden quitar de estas cuentas.  

-   Al instalar un sitio primario, se necesitan los siguientes permisos adicionales:  
    -  **Administrador local** en equipos adicionales en los que vaya a instalar el punto de administración inicial y el punto de distribución, si no se encuentra en el servidor de sitio.  

-   Al instalar un nuevo sitio primario secundario debajo de un sitio de administración central, se necesitan los siguientes permisos adicionales:  

    -   **Administrador local** en el equipo que hospeda el sitio de administración central  

    -   Permisos de administración basada en roles en Configuration Manager equivalentes al rol de seguridad de **Administrador de infraestructura** o **Administrador total**.  

-   Debe usar el medio de instalación correcto (archivos de origen) y ejecutar el programa de instalación desde esa ubicación. Para obtener información sobre los archivos de origen correctos para instalar diferentes sitios, consulte la sección [Opciones para instalar los diferentes tipos de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) del tema [Preparar la instalación de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   El equipo de servidor de sitio debe acceder a los archivos de configuración actualizados de Microsoft:
    -  Antes de comenzar la instalación, puede descargar y almacenar una copia de estos archivos en la red local usando el [descargador del programa de instalación](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Si no hay disponible ninguna copia local de este archivo, el servidor de sitio debe tener acceso a Internet para descargar estos archivos desde Microsoft durante la instalación.

  - Para poder expandir un sitio primario independiente que tenga instalado un rol de sistema de sitio de punto de conexión de servicio, debe desinstalar el punto de conexión de servicio. Se permite solo una instancia de esta función en una jerarquía, y solo en el sitio de nivel superior de la jerarquía. Tendrá la oportunidad de volver a instalar el rol durante la instalación del sitio de administración central.
  - El servidor de sitio y los equipos de bases de datos de sitio deben cumplir todos los requisitos previos de configuración. Antes de iniciar el programa de instalación, puede [ejecutar manualmente el Comprobador de requisitos previos](../../../../core/servers/deploy/install/prerequisite-checker.md) para identificar y corregir problemas.  


## <a name="a-namebkmkexpanda-expanding-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Expandir un sitio primario independiente
Un sitio principal independiente debe cumplir los siguientes requisitos previos antes de que se puede expandir en una jerarquía con un sitio de administración central:


-   **Debe instalar el medio de instalación del nuevo sitio de administración central (archivos de origen) que coincida con la versión del sitio primario independiente:**  
     Para garantizar que las versiones coincidan, instale el sitio nuevo usando los archivos de origen de la [carpeta CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) del sitio primario independiente.

     Para obtener más información sobre los archivos de origen correctos para instalar diferentes sitios, consulte la sección [Opciones para instalar los diferentes tipos de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) del tema [Preparar la instalación de sitios](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **No se puede configurar el sitio primario independiente para migrar datos desde otra jerarquía de Configuration Manager:**  

     Debe detener la migración activa en el sitio primario independiente, de otras jerarquías de Configuration Manager, y quitar todas las configuraciones de migración. Esto incluye los trabajos de migración que no han concluido, la recopilación de datos y la configuración de la jerarquía de origen activa.  

     Esto es necesario porque las operaciones de migración las lleva a cabo el sitio de nivel superior de la jerarquía, por lo que las configuraciones para la migración no se transfieren al sitio de administración central cuando se expande un sitio primario independiente.  

     Después de expandir el sitio primario independiente, si se vuelve a configurar la migración en el sitio primario, será el sitio de administración central el que realice las operaciones relacionadas con la migración. Para obtener más información sobre cómo configurar la migración, consulte [Configurar jerarquías de origen y sitios de origen para la migración a System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **La cuenta del equipo que hospedará el nuevo sitio de administración central debe ser miembro del grupo Administradores del sitio primario independiente:**  

     Para expandir correctamente el sitio primario independiente, la cuenta del equipo del nuevo sitio de administración central debe ser miembro del grupo **Administradores** de los sitios primarios independientes. Esto sólo es necesario durante la expansión del sitio y la cuenta puede quitarse del grupo del sitio primario después de que finalice la expansión del sitio.  

-   **La cuenta de usuario que ejecuta el programa de instalación para instalar el nuevo sitio de administración central debe tener permisos de administración basada en roles en el sitio primario independiente:**  

     Para instalar un sitio de administración central como parte de un escenario de expansión de sitios, la cuenta de usuario que ejecuta el programa de instalación para instalar el sitio de administración central debe definirse en la administración basada en roles en el sitio primario independiente como **Administrador total** o **Administrador de infraestructura**.  

-   **Debe desinstalar los siguientes roles de sistema de sitio del sitio primario independiente antes de que pueda expandir el sitio:**  

    -   Punto de sincronización de Asset Intelligence  

    -   Punto de Endpoint Protection  

    -   Punto de conexión de servicio  

     Estos roles de sistema de sitio se admiten únicamente en el sitio de nivel superior de la jerarquía. Por lo tanto, debe desinstalar estos roles de sistema de sitio antes de expandir el sitio primario independiente. Después de expandir el sitio, puede volver a instalar estos roles de sistema de sitio en el sitio de administración central.  

    Todos los demás roles de sistema de sitio pueden permanecer instalados en el sitio primario.  

-   **El puerto de SQL Server Service Broker debe estar abierto entre el sitio primario independiente y el equipo que se instalará el sitio de administración central:**  

     Para replicar correctamente los datos entre un sitio de administración central y un sitio primario, Configuration Manager requiere que haya abierto un puerto entre los dos sitios que SQL Server Service Broker utilizará. Cuando instale una administración central y expanda un sitio primario independiente, la comprobación de requisito previo no establece que el puerto que especifique para SQL Server Service Broker esté abierto en el sitio primario.  


## <a name="a-namebkmksecondarya-secondary-sites"></a><a name="bkmk_secondary"></a> Sitios secundarios
A continuación se detallan los requisitos previos para instalar los sitios secundarios:
-   El usuario administrativo que configura la instalación del sitio secundario en la consola de Configuration Manager debe tener derechos de administración basada en roles equivalentes al rol de seguridad **Administrador de infraestructura** o **Administrador total**.  

-   La cuenta de equipo del sitio primario principal debe ser un **administrador local** en el equipo del servidor de sitio secundario.  

-   Cuando el sitio secundario utiliza una instancia previamente instalada de SQL Server para hospedar la base de datos del sitio secundario:  

    -   La **cuenta de equipo** del sitio primario principal debe tener derechos de **administrador del sistema** en la instancia de SQL Server del equipo de servidor de sitio secundario.  

    -   La cuenta de **sistema local** del equipo de servidor de sitio secundario debe tener derechos de **administrador del sistema** en la instancia de SQL Server del equipo de servidor de sitio secundario.  

        > [!IMPORTANT]  
        >  Una vez completada la instalación, las dos cuentas deben conservar los derechos de administrador del sistema de SQL Server. Los derechos de administrador del sistema no se pueden quitar de estas cuentas.  

-   El equipo de servidor de sitio secundario debe cumplir todos los requisitos previos de configuración, incluidos SQL Server y los roles de sistema de sitio predeterminados del punto de administración y el punto de distribución.  



<!--HONumber=Nov16_HO1-->


