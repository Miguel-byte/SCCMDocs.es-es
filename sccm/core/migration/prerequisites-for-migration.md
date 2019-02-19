---
title: Requisitos previos de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre las versiones admitidas de Configuration Manager, los idiomas admitidos del sitio de origen y las configuraciones necesarias para llevar a cabo la migración.
ms.date: 5/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6fd2bfda86e7c96f2393c0ca0ea6d1d8ea9f86b4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135465"
---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>Requisitos previos para la migración en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para migrar desde una jerarquía de origen compatible, debe tener acceso a cada sitio de origen de Configuration Manager aplicable. También debe tener permisos en el sitio de destino de System Center Configuration Manager para configurar y ejecutar operaciones de migración.  

 Use la información de las secciones siguientes para conocer las versiones de Configuration Manager compatibles con la migración y las configuraciones necesarias.  

-   [Versiones de Configuration Manager admitidas para la migración](#BKMK_SupportedMigrationVersions)  

-   [Idiomas del sitio de origen que se admiten para la migración](#BKMK_SorceSiteLanguage)  

-   [Configuraciones necesarias para la migración](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> Versiones de Configuration Manager admitidas para la migración  
 Puede migrar datos de una jerarquía de origen que ejecute cualquiera de las siguientes versiones de Configuration Manager:  

- Configuration Manager 2007 SP2 (para los efectos de la migración, Configuration Manager 2007 R2 o R3 en el sitio de origen no se tiene en cuenta. Siempre y cuando el sitio de origen ejecute SP2, se admitirán los sitios que tengan instalado el complemento R2 o R3 para la migración a System Center Configuration Manager).  

- System Center 2012 Configuration Manager SP2 o System Center 2012 R2 Configuration Manager SP1.  

  > [!TIP]  
  >  Además de la migración, puede usar una actualización local de los sitios que ejecutan System Center 2012 Configuration Manager a System Center Configuration Manager.  

- Una jerarquía de System Center Configuration Manager de la misma versión o una inferior de System Center Configuration Manager.  

  Por ejemplo, si tiene una jerarquía de destino que ejecuta System Center Configuration Manager 1606, podría usar la migración para copiar datos de una jerarquía de origen que ejecute la versión 1606 o 1602. Sin embargo, no podría migrar datos de una jerarquía de origen que ejecuta la versión 1610.  


##  <a name="BKMK_SorceSiteLanguage"></a> Idiomas del sitio de origen que se admiten para la migración  
 Cuando migra datos entre jerarquías de Configuration Manager, estos se almacenan en la jerarquía de destino en el formato independiente del idioma para System Center Configuration Manager. Debido a que Configuration Manager 2007 no almacena datos en un formato neutral de idioma, el proceso de migración debe convertir los objetos a este formato durante la migración de Configuration Manager 2007. Por lo tanto, solo los sitios de origen de Configuration Manager 2007 que se instalan con los siguientes idiomas son compatibles con la migración:  

-   Inglés  

-   Francés  

-   Alemán  

-   Japonés  

-   Coreano  

-   Ruso  

-   Chino simplificado  

-   Chino tradicional  

Al migrar datos desde una jerarquía de System Center 2012 Configuration Manager o de System Center Configuration Manager, no hay ninguna limitación en los idiomas del sitio de origen. Los objetos de la base de datos del sitio de origen ya están en un formato neutral de idioma.  

##  <a name="BKMK_Required_Configurations"></a> Configuraciones necesarias para la migración  
A continuación, se enumeran las configuraciones necesarias para el uso de la migración y las operaciones de migración:  

- **Para configurar, ejecutar y supervisar la migración en la consola de Configuration Manager:**  

   En el sitio de destino, su cuenta debe tener asignado el rol de seguridad de administración basada en roles de **Administrador de infraestructuras**. Este rol de seguridad concede permisos para administrar todas las operaciones de migración, lo que incluye la creación de trabajos de migración, limpieza, supervisión, y la acción de compartir y actualizar puntos de distribución.  

- **Recopilación de datos:**  

   Para permitir que el sitio de destino recopile datos, debe configurar las dos cuentas de acceso del sitio de origen siguientes para su uso con cada sitio de origen:  

  -   **Cuenta de sitio de origen:** Esta cuenta se usa para tener acceso al proveedor de SMS del sitio de origen.  

      -   Para un sitio de origen de Configuration Manager 2007 SP2, esta cuenta necesita el permiso **Leer** para todos los objetos del sitio de origen.  

      -   Para un sitio de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, esta cuenta requiere el permiso **Leer** para todos los objetos del sitio de origen. Este permiso se concede a la cuenta mediante administración basada en roles. Para obtener información sobre cómo usar la administración basada en roles, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md) (Conceptos básicos de la administración basada en roles de System Center Configuration Manager).  

  -   **Cuenta de base de datos del sitio de origen:** esta cuenta se usa para tener acceso a la base de datos de SQL Server del sitio de origen y necesita los permisos **Conectar**, **Ejecutar** y **Seleccionar** para la base de datos del sitio de origen.  

  Puede configurar estas cuentas cuando configure una nueva jerarquía de origen, cuando configure la recopilación de datos para un sitio de origen adicional o cuando vuelva a configurar las credenciales para un sitio de origen. Estas cuentas pueden utilizar una cuenta de usuario de dominio, o puede especificar la cuenta de equipo del sitio de nivel superior de la jerarquía de destino.  

  > [!IMPORTANT]  
  >  Si usa la cuenta de equipo de Configuration Manager, asegúrese de que esta cuenta forma parte del grupo de seguridad **Usuarios COM distribuidos** en el dominio donde reside el sitio de origen.  

  Al recopilar datos, se utilizan los puertos y protocolos de red siguientes:  

  -   NetBIOS/SMB - 445 (TCP)  

  -   RPC (WMI) - 135 (TCP)  

  -   SQL Server - los puertos TCP que utilizan bases de datos de sitios de origen y de destino.  

- **Migrar actualizaciones de software:**  

   Antes de migrar actualizaciones de software, debe configurar la jerarquía de destino con un punto de actualización de software. Para obtener más información, consulte [Planeación de la migración de actualizaciones de software](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

- **Compartir puntos de distribución:**  

   Para compartir correctamente cualquier punto de distribución de un sitio de origen, al menos un sitio primario o el sitio de administración central de la jerarquía de destino debe usar los mismos números de puerto para las solicitudes de cliente que el sitio de origen. Para obtener información sobre los puertos de solicitud de cliente, consulte [How to configure client communication ports in System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md) (Configurar puertos de comunicación de cliente en System Center Configuration Manager).  

   Para cada sitio de origen, solo se comparten los puntos de distribución que se instalan en los servidores del sistema de sitio que se configuran con un FQDN.  

   Además, para compartir un punto de distribución de un sitio de origen de System Center 2012 Configuration Manager o System Center Configuration Manager, la **cuenta de sitio de origen** (que obtiene acceso al proveedor de SMS del servidor del sitio de origen) debe tener permisos de **modificación** en el objeto **Sitio** del sitio de origen. Este permiso se concede a la cuenta mediante la administración basada en roles. Para obtener información sobre cómo usar la administración basada en roles, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md) (Conceptos básicos de la administración basada en roles de System Center Configuration Manager).  


- **Actualizar o volver a asignar puntos de distribución:**  

   La **Cuenta de acceso del sitio de origen** configurada para recopilar datos del proveedor de SMS del sitio de origen debe tener los permisos siguientes:  

  - Para actualizar un punto de distribución de Configuration Manager 2007, la cuenta necesita los permisos **Leer**, **Ejecutar** y **Eliminar** en la clase **Sitio** en el servidor de sitio de Configuration Manager 2007 para quitar correctamente el punto de distribución del sitio de origen de Configuration Manager 2007.  

  - Para reasignar un punto de distribución de System Center 2012 Configuration Manager o de System Center Configuration Manager, la cuenta debe tener el permiso **Modificar** para el objeto **Sitio** en el sitio de origen. Este permiso se concede a la cuenta mediante la administración basada en roles. Para obtener información sobre cómo usar la administración basada en roles, consulte [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md) (Conceptos básicos de la administración basada en roles de System Center Configuration Manager).  

    Para actualizar o reasignar correctamente un punto de distribución a una nueva jerarquía, los puertos que se configuran para solicitudes de clientes, en el sitio que administra el punto de distribución de la jerarquía de origen, deben coincidir con los puertos que se configuran para solicitudes de clientes en el sitio de destino que administrará el punto de distribución. Para obtener información sobre los puertos de solicitud de cliente, consulte [How to configure client communication ports in System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md) (Configurar puertos de comunicación de cliente en System Center Configuration Manager).  
