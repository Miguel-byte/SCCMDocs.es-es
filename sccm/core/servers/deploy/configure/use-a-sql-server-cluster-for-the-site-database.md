---
title: "Clúster de SQL Server | Microsoft Docs"
description: "Use un clúster de SQL Server para hospedar la base de datos de sitio de System Center Configuration Manager. Incluye información sobre las opciones admitidas."
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: 10
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ce0d7fc5f3d1812c4d62e551661c0ef89707567b
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.lasthandoff: 02/28/2017


---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Usar un clúster de SQL Server para la base de datos de sitio de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


 Puede usar un clúster de SQL Server para hospedar la base de datos de sitio de System Center Configuration Manager. La base de datos del sitio es el único rol de sistema de sitio admitido en un clúster de servidores.  

> [!IMPORTANT]  
>  La configuración correcta de los clústeres de SQL Server se basa en la documentación y los procedimientos proporcionados en la biblioteca de documentación de SQL Server.  

 Un clúster puede proporcionar compatibilidad con la conmutación por error y mejorar la confiabilidad de la base de datos del sitio, pero no ofrece un procesamiento adicional ni ventajas de equilibrio de carga. De hecho, el rendimiento puede degradarse porque el servidor de sitio debe encontrar el nodo activo del clúster de SQL Server antes de conectarse a la base de datos del sitio.  

 Antes de instalar Configuration Manager, debe preparar el clúster de SQL Server para que admita Configuration Manager. (Consulte los requisitos previos más adelante en esta sección).  

 Durante la instalación de Configuration Manager, el escritor del Servicio de instantáneas de volumen de Windows se instala en cada nodo de equipo físico del clúster de Microsoft Windows Server. De este modo, se admite la tarea de mantenimiento de **Copia de seguridad del servidor del sitio**.  

 Una vez instalado el sitio, Configuration Manager comprueba cada hora los cambios que se producen en el nodo de clúster. Configuration Manager administra automáticamente los cambios que se encuentran y que afectan a las instalaciones de componentes de Configuration Manager (como una conmutación por error de nodo o la adición de un nuevo nodo al clúster de SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Opciones admitidas para el uso de un clúster de conmutación por error de SQL Server

Se admiten las siguientes opciones para los clústeres de conmutación por error de SQL Server usados como base de datos del sitio:

-   Clúster de instancia única  

-   Configuración de varias instancias  

-   Varios nodos activos  

-   Instancia con nombre o instancia predeterminada  

Tenga en cuenta los siguientes requisitos previos:  

-   La base de datos del sitio debe ser remota con respecto al servidor de sitio. (El clúster no puede incluir el servidor de sistema de sitio).  

-   Debe agregar la cuenta de equipo del servidor de sitio al grupo de administradores locales de cada servidor del clúster.  

-   Para admitir la autenticación Kerberos, el protocolo de comunicación de red **TCP/IP** debe estar habilitado para la conexión de red de cada nodo del clúster de SQL Server. No hacen falta**canalizaciones con nombre** , pero pueden usarse para solucionar problemas de autenticación Kerberos. Las opciones de protocolo de red se configuran en **Administrador de configuración de SQL Server**, en **Configuración de red de SQL Server**.  

-   Si usa una PKI, vea Requisitos de certificados PKI para Configuration Manager para conocer los requisitos de certificado específicos cuando se usa un clúster de SQL Server para la base de datos del sitio.  

Tenga en cuenta las limitaciones siguientes:  

-   **Instalación y configuración:**  

    -   Los sitios secundarios no pueden usar un clúster de SQL Server.  

    -   La opción de especificar ubicaciones de archivos no predeterminadas para la base de datos del sitio no está disponible cuando se especifica un clúster de SQL Server.  

-   **Proveedor de SMS:**  

    -   No se admite la instalación de una instancia del proveedor de SMS en un clúster de SQL Server ni en un equipo que se ejecuta como un nodo de SQL Server en clúster.  

-   **Opciones de replicación de datos:**  

    -   Si va a usar **vistas distribuidas**, no puede usar un clúster de SQL Server para hospedar la base de datos del sitio.  

-   **Copia de seguridad y recuperación:**  

    -   Configuration Manager no admite la copia de seguridad de Data Protection Manager (DPM) para un clúster de SQL Server que use una instancia con nombre. En cambio, admite la copia de seguridad de DPM en un clúster de SQL Server que use la instancia predeterminada de SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Preparar una instancia de SQL Server en clúster para la base de datos del sitio  

Estas son las principales tareas que debe llevar a cabo para preparar la base de datos del sitio:

-   Cree el clúster virtual de SQL Server para hospedar la base de datos del sitio en un entorno de clúster de Windows Server existente. Para conocer pasos específicos para instalar y configurar un clúster de SQL Server, vea la documentación específica de la versión de SQL Server. Por ejemplo, si utiliza SQL Server 2008 R2, consulte [Installing a SQL Server 2008 R2 Failover Cluster (Instalación de un clúster de conmutación por error de SQL Server 2008 R2)](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   En cada equipo del clúster de SQL Server puede colocar un archivo en la carpeta raíz de cada unidad en donde no quiere que Configuration Manager instale componentes del sitio. El archivo debe denominarse **NO_SMS_ON_DRIVE.SMS**. De forma predeterminada, Configuration Manager instala algunos componentes en cada nodo físico para admitir operaciones como la copia de seguridad.  

-   Agregue la cuenta de equipo del servidor de sitio al grupo de **administradores locales** de cada equipo de nodo de clúster de Windows Server.  

-   En la instancia virtual de SQL Server, asigne el rol **sysadmin** de SQL Server a la cuenta de usuario que ejecutará el programa de instalación de Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Para instalar un sitio nuevo con un servidor de SQL Server en clúster  
 Para instalar un sitio que usa una base de datos del sitio en clúster, ejecute el programa de instalación de Configuration Manager siguiendo el proceso normal para instalar un sitio, pero introduzca la modificación siguiente:  

-   En la página **Información de base de datos** , especifique el nombre de la instancia virtual de clúster de SQL Server que hospedará la base de datos del sitio. La instancia virtual reemplaza el nombre del equipo que ejecuta SQL Server.  

    > [!IMPORTANT]  
    >  Cuando escriba el nombre de la instancia virtual de clúster de SQL Server, no escriba el nombre virtual de Windows Server creado por el clúster de Windows Server. Si usa el nombre virtual de Windows Server, la base de datos del sitio se instala en la unidad de disco duro local del nodo de clúster activo de Windows Server. Esto impide que la conmutación por error se lleve a cabo correctamente si se produce un error en ese nodo.  

