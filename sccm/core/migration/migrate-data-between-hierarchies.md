---
title: Migrar datos | Microsoft Docs
description: "Obtenga información acerca de cómo transferir datos desde una jerarquía de origen a una jerarquía de destino de System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: 11
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a8959c72608a1531fb323176c33a848a4a669b1c
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc


---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Migrar datos entre jerarquías en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Utilice la migración para transferir datos desde una jerarquía de origen compatible a la jerarquía de destino de System Center Configuration Manager.  Al migrar datos desde una jerarquía de origen:  

-   Acceda a los datos de las bases de datos de sitio que identifique en la infraestructura de origen y luego transfiera los datos a su entorno actual.  

-   La migración no cambia los datos en la jerarquía de origen, sino que detecta los datos y almacena una copia de los mismos en la base de datos de la jerarquía de destino.  

Tenga en cuenta lo siguiente al planear la estrategia de migración:  

-   Puede migrar una infraestructura existente de Configuration Manager 2007 SP2 a System Center Configuration Manager.  

-   Puede migrar algunos de los datos compatibles (o todos) desde un sitio de origen.  

-   Puede migrar los datos desde un sitio de origen único a varios sitios de la jerarquía de destino.  

-   Puede mover datos desde varios sitios de origen a un único sitio de la jerarquía de destino.  

##  <a name="a-namebkmkmigrationconceptsa-concepts-for-migration"></a><a name="BKMK_MigrationConcepts"></a> Conceptos de la migración  
 Es posible que encuentre los conceptos y términos siguientes cuando use la migración.  

|Concepto o término|Más información|  
|---------------------|----------------------|  
|Jerarquía de origen|Una jerarquía que ejecuta una versión compatible de Configuration Manager y que tiene los datos que se van a migrar. Cuando se configura la migración, se identifica la jerarquía de origen al especificar el sitio de nivel superior de una jerarquía de origen. Después de especificar una jerarquía de origen, el sitio de nivel superior de la jerarquía de destino recopila datos de la base de datos del sitio de origen designado para identificar los datos que desea migrar.<br /><br /> Para más información, vea [Jerarquías de origen](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) en [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Sitios de origen|Son los sitios en la jerarquía de origen que tienen los datos que puede migrar a su jerarquía de destino.<br /><br /> Para más información, vea [Sitios de origen](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) en [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Jerarquía de destino|Una jerarquía de System Center Configuration Manager en la que se ejecuta la migración para importar datos de una jerarquía de origen.|  
|Recopilación de datos|Es el proceso continuo de identificar la información en una jerarquía de origen que se pueden migrar a la jerarquía de destino. Configuration Manager comprueba la jerarquía de origen según una programación establecida para identificar cambios en la información de la jerarquía de origen que se migró anteriormente y que puede querer actualizar en la jerarquía de destino.<br /><br /> Para más información, vea [Recopilación de datos](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) en [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Trabajos de migración|El proceso de configuración de los objetos que se desea migrar y la posterior administración de la migración de dichos objetos a la jerarquía de destino.<br /><br /> Para obtener más información, vea [Planning a migration job strategy in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md) (Planeación de una estrategia de trabajo de migración en System Center Configuration Manager).|  
|Migración de clientes|El proceso de transferencia de información que los clientes usan desde la base de datos del sitio de origen hasta la base de datos de la jerarquía de destino. Esta migración de datos va seguida de una actualización del software cliente de dispositivos a la versión del software cliente de la jerarquía de destino.<br /><br /> Para obtener más información, vea [Planning a client migration strategy in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Puntos de distribución compartidos|Los puntos de distribución de la jerarquía de origen que se comparten con la jerarquía de destino durante la migración.<br /><br /> Durante la migración, los clientes asignados a sitios en la jerarquía de destino pueden obtener contenido de los puntos de distribución compartidos.<br /><br /> Para más información, vea [Compartir puntos de distribución entre jerarquías de origen y de destino](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) en [Planear una estrategia de migración de implementación de contenido en System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Supervisión de la migración|Es el proceso de supervisión de las actividades de migración. Debe supervisar el progreso y la correcta finalización de la migración desde el nodo **Migración** en el área de trabajo **Administración**.<br /><br /> Para obtener más información, vea [Planning to monitor migration activity in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md) (Planeación para supervisar la actividad de migración en System Center Configuration Manager).|  
|Detener la recopilación de datos|Es el proceso de detener la recopilación de datos de sitios de origen. Cuando ya no hay datos de una jerarquía de origen que quiere migrar, o si quiere pausar las actividades relacionadas con la migración, puede configurar la jerarquía de destino para que deje de recopilar datos de la jerarquía de origen.<br /><br /> Para más información, vea [Recopilación de datos](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) en [Planear una estrategia de jerarquía de origen en System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Limpiar datos de migración|Es el proceso de finalización de la migración de una jerarquía de origen mediante la eliminación de la información sobre la migración de la base de datos de las jerarquías de destino.<br /><br /> Para obtener más información, vea [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Flujo de trabajo de migración típico  
Para configurar un flujo de trabajo para la migración:

1.  Especifique una jerarquía de origen compatible.  

2.  Configure la recopilación de datos. La recopilación de datos permite a Configuration Manager recopilar información sobre los datos que se pueden migrar desde la jerarquía de origen.  

     Configuration Manager automáticamente repite el proceso para recopilar datos según una programación simple hasta que detenga el proceso de recopilación de datos. De manera predeterminada, el proceso de recopilación de datos se repite cada cuatro horas para que Configuration Manager pueda identificar cambios en los datos de la jerarquía de origen que pueda querer migrar. La recopilación de datos también es necesaria para compartir puntos de distribución de la jerarquía de origen a la jerarquía de destino.  

3.  Cree trabajos de migración para migrar datos entre la jerarquía de origen y la jerarquía de destino.  

4.  Puede detener la recopilación de datos en cualquier momento mediante el comando **Detener la recopilación de datos** . Cuando se detiene la recopilación de datos, Configuration Manager deja de identificar cambios en los datos de la jerarquía de origen y no podrá seguir compartiendo puntos de distribución entre la jerarquía de origen y la jerarquía de destino. Normalmente, se usa esta acción cuando ya no va a migrar datos o a compartir puntos de distribución de la jerarquía de origen.  

5.  Opcionalmente, después de detener la recopilación de datos de todos los sitios de la jerarquía de origen, puede limpiar los datos de migración mediante el comando **Limpiar datos de migración** . Este comando elimina datos históricos de migración de una jerarquía de origen de la base de datos de la jerarquía de destino.  

Después de migrar los datos de una jerarquía de origen de Configuration Manager que ya no volverá a usar para administrar el entorno, puede retirar la jerarquía de origen y la infraestructura.  

##  <a name="a-namebkmkmigrationscenariosa-migration-scenarios"></a><a name="BKMK_MigrationScenarios"></a> Escenarios de migración  
 Configuration Manager admite los siguientes escenarios de migración.  

> [!NOTE]  
>  La expansión de una jerarquía que tiene un sitio independiente a una jerarquía que tiene un sitio de administración central no se considera una migración. Para más información sobre la expansión de jerarquías, vea [Expandir un sitio primario independiente](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) en [Usar el Asistente para instalación para instalar sitios](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migración desde jerarquías de Configuration Manager 2007  
 Cuando usa la migración para migrar datos desde Configuration Manager 2007, puede mantener la inversión en la infraestructura de sitio existente y obtener las ventajas siguientes:  

|Ventaja|Más información|  
|-------------|----------------------|  
|Mejoras de la base de datos del sitio|La base de datos de System Center Configuration Manager es plenamente compatible con Unicode.|  
|Replicación de base de datos entre sitios|La replicación en System Center Configuration Manager se basa en Microsoft SQL Server. Esto mejora el rendimiento de la transferencia de datos entre sitios.|  
|Administración centrada en el usuario|Los usuarios son el centro de las tareas de administración de System Center Configuration Manager. Por ejemplo, puede distribuir software a un usuario incluso si no conoce el nombre del dispositivo para ese usuario. Además, System Center Configuration Manager proporciona a los usuarios un mayor control sobre el software que se instala en los dispositivos y cuándo se instala dicho software.|  
|Simplificación de la jerarquía|En System Center Configuration Manager, el tipo de sitio de administración central y los cambios en el comportamiento de los sitios primarios y secundarios le permite generar una jerarquía de sitio más simple, que usa menos ancho de banda y requiere menos servidores.|  
|Administración basada en roles|Este modelo de seguridad central en System Center Configuration Manager ofrece seguridad y administración a nivel de jerarquía según sus requisitos administrativos y empresariales.|  

> [!NOTE]  
>  Debido a los cambios de diseño que se introdujeron en System Center 2012 Configuration Manager, no puede actualizar la infraestructura de Configuration Manager 2007 a System Center Configuration Manager. Se admite la actualización in situ de System Center 2012 Configuration Manager a System Center Configuration Manager.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migración desde Configuration Manager 2012 o desde otra jerarquía de System Center Configuration Manager  
 El proceso de migración de datos de una jerarquía de System Center 2012 Configuration Manager o System Center Configuration Manager es el mismo. Incluye la migración de datos de varias jerarquías de origen a una sola jerarquía de destino, como cuando su compañía adquiere recursos adicionales ya administrados por Configuration Manager. Además, puede migrar datos de un entorno de prueba a un entorno de producción de Configuration Manager. Esto le permite mantener su inversión en el entorno de prueba de Configuration Manager.  

## <a name="additional-topics-for-migration"></a>Temas adicionales sobre migración:  

-   [Planning for migration to System Center Configuration Manager](../../core/migration/planning-for-migration.md) (Planeación de la migración a System Center Configuration Manager)  

-   [Configuring source hierarchies and source sites for migration to System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md) (Configuración de jerarquías y sitios de origen para la migración a System Center Configuration Manager)  

-   [Operations for migrating to System Center Configuration Manager](../../core/migration/operations-for-migration.md) (Operaciones para migrar a System Center Configuration Manager)  

-   [Security and privacy for migration to System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md) (Seguridad y privacidad de la migración a System Center Configuration Manager)  

## <a name="see-also"></a>Véase también  
 [Start using System Center Configuration Manager](../../core/servers/deploy/start-using.md) (Inicio del uso en System Center Configuration Manager)



<!--HONumber=Dec16_HO5-->


