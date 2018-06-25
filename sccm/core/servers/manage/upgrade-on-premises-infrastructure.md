---
title: Actualizar la infraestructura local
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo actualizar la infraestructura, como SQL Server y el sistema operativo de sistemas de sitio.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc433d63eb647ef7a0a88ada212f949783ac25c0
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474258"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Actualizar la infraestructura local que es compatible con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use la información de este artículo para ayudarle a actualizar la infraestructura del servidor que ejecuta Configuration Manager.  

 - Si quiere *actualizar* desde una versión anterior de Configuration Manager a System Center Configuration Manager, rama actual, vea [Actualizar a System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Si quiere *actualizar* la infraestructura de System Center Configuration Manager, rama actual, a una nueva versión, vea [Actualizaciones para System Center Configuration Manager](/sccm/core/servers/manage/updates).



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Actualización del sistema operativo de los sistemas de sitio  
 Configuration Manager admite la actualización local del sistema operativo (SO) de los servidores que hospedan un servidor de sitio y de los servidores remotos que hospedan cualquier rol de sistema de sitio en las situaciones siguientes:  

-   Actualización local a un Service Pack posterior de Windows Server si el nivel de Service Pack resultante de Windows sigue siendo compatible con Configuration Manager.  
-   Actualización local desde:
    - Windows Server 2012 R2 a Windows Server 2016 ([ver detalles adicionales](#bkmk_2016)).
    - Windows Server 2012 a Windows Server 2016 ([ver detalles adicionales](#bkmk_2016)).
    - Windows Server 2012 a Windows Server 2012 R2 ([ver detalles adicionales](#bkmk_2012r2)).
    - Windows Server 2008 R2 a Windows Server 2012 R2 ([ver detalles adicionales](#bkmk_from2008r2)).

    > [!WARNING]  
    >  Antes de actualizar a un sistema operativo diferente, *debe desinstalar WSUS* del servidor. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS. Para más información sobre este paso crítico, consulte la sección "Funcionalidad nueva y modificada" en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.  

Para actualizar un servidor, use los procedimientos de actualización que proporciona el SO al que se va a actualizar. Vea los siguientes artículos:
  -  [Opciones de actualización para Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) en la documentación de Windows Server.  
  - [Opciones de actualización y conversión para Windows Server 2016](/windows-server/get-started/supported-upgrade-paths) en la documentación de Windows Server.

### <a name="bkmk_2016"></a> Actualización de Windows Server 2012 o Windows Server 2012 R2 a 2016
Al actualizar Windows Server 2012 o Windows Server 2012 R2 a Windows Server 2016, hay que tener en cuenta lo siguiente:


#### <a name="before-upgrade"></a>Antes de la actualización  
-   Quite el cliente de System Center Endpoint Protection (SCEP). Windows Server 2016 tiene Windows Defender integrado, que reemplaza al cliente SCEP. La presencia del cliente SCEP puede impedir la actualización a Windows Server 2016.
-   Quite el rol de WSUS del servidor si está instalado. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS.

#### <a name="after-upgrade"></a>Después de la actualización   
-   Asegúrese de que Windows Defender está habilitado, establecido para el inicio automático y en ejecución.
-   Asegúrese de que se ejecutan los siguientes servicios de Configuration Manager:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
  -     Servidor de sitio
  -     Punto de administración
  -     Punto de servicio web del catálogo de aplicaciones
  -     Punto de sitios web del catálogo de aplicaciones

-   Asegúrese de que todos los servidores que hospeden un rol de sistema de sitio sigan cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecuten en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

-   Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se hayan iniciado y estén operativos.

-   Si va a actualizar el servidor de sitio primario, [ejecute un restablecimiento de sitio](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema conocido de consolas remotas de Configuration Manager   
Después de actualizar el servidor de sitio o un servidor que hospeda una instancia de SMS_Provider para Windows Server 2016, es posible que los usuarios administrativos no puedan conectar una consola de Configuration Manager al sitio. Para evitar este problema, debe restaurar de forma manual los permisos del grupo de administradores de SMS en WMI. Los permisos deben establecerse en el servidor de sitio y en cada servidor remoto que hospede una instancia del proveedor de SMS:

1. En los servidores aplicables, abra Microsoft Management Console (MMC), agregue el complemento de **Control WMI** y, luego, seleccione **Equipo local**.
2. En MMC, abra las **Propiedades** de **Control WMI (local)** y seleccione la pestaña **Seguridad**.
3. Expanda el árbol por debajo de la raíz, seleccione el nodo **SMS** y, luego, elija **Seguridad**.  Asegúrese de que el grupo **Administradores de SMS** tiene los permisos siguientes:
  -     Habilitar cuenta
  -     Llamada remota habilitada
4. En la pestaña **Seguridad**, en el nodo **SMS**, seleccione el nodo **sitio_&lt;CódigoDeSitio** y, después, elija **Seguridad**. Asegúrese de que el grupo **Administradores de SMS** tiene los permisos siguientes:
  -   Ejecutar métodos
  -   Escritura de proveedor
  -   Habilitar cuenta
  -   Llamada remota habilitada
5. Guarde los permisos para restaurar el acceso de la consola de Configuration Manager.


### <a name="bkmk_2012r2"></a> Windows Server 2012 a Windows Server 2012 R2

#### <a name="before-upgrade"></a>Antes de la actualización  
-   Quite el rol de WSUS del servidor si está instalado. Puede mantener el SUSDB y readjuntarlo una vez que se vuelva a instalar WSUS.

#### <a name="after-upgrade"></a>Después de la actualización  
  - Asegúrese de que los servicios de implementación de Windows están iniciados y en ejecución para los siguientes roles de sistema de sitio (este servicio se detiene durante la actualización):
    - Servidor de sitio
    - Punto de administración
    - Punto de servicio web del catálogo de aplicaciones
    - Punto de sitios web del catálogo de aplicaciones

  -     Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
    -   Servidor de sitio
    -   Punto de administración
    -   Punto de servicio web del catálogo de aplicaciones
    -   Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que todos los servidores que hospeden un rol de sistema de sitio sigan cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecuten en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

  Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se hayan iniciado y estén operativos.

### <a name="bkmk_from2008r2"></a> Actualización de Windows Server 2008 R2 a Windows Server 2012 R2
Este escenario de actualización de SO tiene las siguientes condiciones:  

#### <a name="before-upgrade"></a>Antes de la actualización  
-   Desinstale WSUS 3.2.  
    Antes de actualizar un SO de servidor a Windows Server 2012 R2, debe desinstalar WSUS 3.2 del servidor. Para más información sobre este paso crítico, consulte la sección Funcionalidad nueva y modificada en [Introducción a Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) en la documentación de Windows Server.

#### <a name="after-upgrade"></a>Después de la actualización  
  - Asegúrese de que los servicios de implementación de Windows están iniciados y en ejecución para los siguientes roles de sistema de sitio (este servicio se detiene durante la actualización):
    - Servidor de sitio
    - Punto de administración
    - Punto de servicio web del catálogo de aplicaciones
    - Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que los servicios **Activación de proceso de Windows** y **WWW/W3svc** están habilitados, establecidos para el inicio automático y en ejecución en los siguientes roles de sistema de sitio (estos servicios se deshabilitan durante la actualización):
    -   Servidor de sitio
    -   Punto de administración
    -   Punto de servicio web del catálogo de aplicaciones
    -   Punto de sitios web del catálogo de aplicaciones


  -     Asegúrese de que todos los servidores que hospedan un rol de sistema de sitio siguen cumpliendo todos los [requisitos previos para roles de sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) que se ejecutan en ese servidor. Por ejemplo, puede que tenga que volver a instalar BITS, WSUS, o configurar valores específicos de IIS.

  Después de restaurar los requisitos previos que falten, reinicie el servidor una vez más para asegurarse de que los servicios se hayan iniciado y estén operativos.


### <a name="unsupported-upgrade-scenarios"></a>Escenarios de actualización no compatibles
Con frecuencia, se pregunta sobre los siguientes escenarios de actualización de Windows Server, pero no son compatibles con Configuration Manager:  

-   Windows Server 2008 a Windows Server 2012 o posterior  
-   Windows Server 2008 R2 a Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Actualizar el SO de clientes de Configuration Manager  
 Configuration Manager admite una actualización local del SO para los clientes de Configuration Manager en las situaciones siguientes:  

-   Actualización local a un Service Pack posterior de Windows si el nivel de Service Pack resultante sigue siendo compatible con Configuration Manager.  

-   Actualización inmediata de Windows desde una versión compatible a Windows 10. Para más información, consulte [Actualizar Windows a la versión más reciente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Actualizaciones de mantenimiento desde una compilación a otra de Windows 10. Para obtener más información, consulte [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md) (Administrar Windows como servicio).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Actualizar SQL Server en el servidor de base de datos del sitio  
  Configuration Manager admite una actualización local de SQL Server desde una versión compatible de SQL en el servidor de base de datos del sitio. Los escenarios de actualización de SQL Server que encontrará en esta sección son compatibles con Configuration Manager e incluyen los requisitos de cada uno de ellos.

 Para más información sobre las versiones de SQL Server compatibles con Configuration Manager, consulte [Versiones de SQL Server compatibles con System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 ### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Actualizar la versión del Service Pack de SQL Server    
 Configuration Manager admite la actualización local de SQL Server a un Service Pack posterior si el nivel de Service Pack resultante de SQL Server sigue siendo compatible con Configuration Manager.

 Cuando tenga varios sitios de Configuration Manager en una jerarquía, cada sitio puede ejecutar una versión de Service Pack de SQL Server diferente. No hay ninguna limitación en el orden en el que los sitios actualizan la versión del Service Pack de SQL Server que se utiliza para la base de datos del sitio.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Actualización a una nueva versión de SQL Server   
 Configuration Manager es compatible con la actualización local de SQL Server a las siguientes versiones:

 - SQL Server 2017
 - SQL Server 2016  
 - SQL Server 2014  

Al actualizar la versión de SQL Server que hospeda la base de datos de sitio, debe actualizar la versión de SQL Server que se usa en los sitios en el siguiente orden:

 1. Actualice primero SQL Server en el sitio de administración central.
 2. Actualice los sitios secundarios antes de actualizar un sitio primario principal de un sitio secundario.
 3. Actualice los sitios primarios principales en último lugar. Estos sitios incluyen tanto los sitios primarios secundarios, que informan a un sitio de administración central, como los sitios primarios independientes, que están en el sitio de nivel superior de una jerarquía.

### <a name="sql-server-cardinality-estimation-level-and-the-site-database"></a>Nivel de estimación de cardinalidad de SQL Server y la base de datos del sitio   
Cuando una base de datos del sitio se actualiza de una versión anterior de SQL Server, la base de datos conserva su nivel existente de estimación de cardinalidad (CE) de SQL si se encuentra en el mínimo permitido para esa instancia de SQL Server. La actualización de SQL Server con una base de datos en un nivel de compatibilidad inferior al nivel permitido establece automáticamente la base de datos en el nivel de compatibilidad más bajo que permite SQL Server.

En la tabla siguiente se identifican los niveles de compatibilidad recomendados para las bases de datos del sitio de Configuration Manager:

|Versión de SQL Server | Niveles de compatibilidad admitidos |Nivel recomendado|
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Para identificar el nivel de compatibilidad de CE de SQL Server en uso para la base de datos del sitio, ejecute la siguiente consulta SQL en el servidor de base de datos del sitio:  
`SELECT name, compatibility_level FROM sys.databases`

 Para obtener más información sobre los niveles de compatibilidad de CE de SQL y cómo establecerlos, consulte [Nivel de compatibilidad de ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Para más información sobre la actualización de SQL Server, consulte la siguiente documentación de SQL Server:
-   [Actualización a SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [Actualización a SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [Actualización a SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Para actualizar SQL Server en el servidor de base de datos del sitio  

1.  Detenga todos los servicios de Configuration Manager del sitio.  
2.  Actualice SQL Server a una versión compatible.  
3.  Reinicie los servicios de Configuration Manager.  

> [!NOTE]  
>  Al cambiar la edición de SQL Server en uso en el sitio de administración central desde una edición Standard a la edición Enterprise o Datacenter, la partición de la base de datos que limita el número de clientes que admite la jerarquía no cambia.
