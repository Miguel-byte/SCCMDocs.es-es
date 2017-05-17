---
title: Crear colecciones | Microsoft Docs
description: "Cree recopilaciones en System Center Configuration Manager para facilitar la administración de grupos de usuarios y dispositivos."
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 9555a16d97224a1cf49a426ab225468b07403f60
ms.openlocfilehash: e28fdeae809cadf78017dd2920e3f1a9484ec8a3
ms.contentlocale: es-es
ms.lasthandoff: 12/29/2016


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Cómo crear recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las recopilaciones son grupos de usuarios o dispositivos. Use las recopilaciones para tareas como la administración de aplicaciones, la implementación de la configuración de cumplimiento o la instalación de actualizaciones de software. También puede utilizar las recopilaciones para administrar grupos de configuraciones de cliente o usarlas con administración basada en roles para especificar recursos a los que puede un usuario administrativo puede acceder. Configuration Manager contiene varias recopilaciones integradas. Para obtener más información, consulte [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md) (Introducción a las recopilaciones en System Center Configuration Manager).  

> [!NOTE]  
>  Una recopilación puede contener usuarios o dispositivos, pero no ambos.  

 En la tabla siguiente, se enumeran las reglas que puede usar para configurar los miembros de una recopilación en Configuration Manager.  

|Tipo de regla de pertenencia|Más información|  
|--------------------------|----------------------|  
|Regla directa|Elija los usuarios o equipos que quiera agregar a una recopilación. Esta pertenencia no cambia a menos que quite un recurso de Configuration Manager. Configuration Manager debe haber detectado los recursos o se deben haber importado los recursos antes de poderlos agregar a una recopilación de regla directa. Las recopilaciones de reglas directas tienen una mayor carga administrativa que las recopilaciones de reglas de consulta porque requieren cambios manuales.|  
|Regla de consulta|Actualice de forma dinámica la pertenencia de una recopilación basándose en una consulta que Configuration Manager ejecuta según una programación. Por ejemplo, puede crear una recopilación de usuarios que sean miembros de la unidad organizativa Recursos humanos de los Servicios de dominio de Active Directory. Esta recopilación se actualiza automáticamente cuando se agregan usuarios nuevos o se quitan usuarios de la unidad organizativa Recursos humanos.<br /><br /> Para obtener consultas de ejemplo que puede usar para crear recopilaciones, consulte [How to create queries in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md) (Cómo crear consultas en System Center Configuration Manager).|  
|Regla de inclusión de recopilación|Incluya los miembros de otra recopilación en una recopilación de Configuration Manager. La pertenencia de la recopilación actual se actualiza según una programación si la recopilación incluida cambia.<br /><br /> Puede agregar varias reglas de inclusión de recopilación a una recopilación.<br /> |  
|Regla de exclusión de recopilación|La regla de exclusión de recopilación le permite excluir los miembros de otra recopilación de una recopilación de Configuration Manager. La pertenencia de la recopilación actual se actualiza según una programación si la recopilación excluida cambia.<br /><br /> Puede agregar varias reglas de exclusión de recopilación a una recopilación. Si una recopilación incluye tanto reglas de inclusión de recopilación como reglas de exclusión de recopilación y se produce un conflicto, la regla de exclusión tiene prioridad.<br />              **Ejemplo:** se crea una recopilación que tiene una regla de inclusión de recopilación y una regla de exclusión de recopilación. La regla de inclusión de recopilación es para una recopilación de equipos de escritorio de Dell. La de exclusión de recopilación es una recopilación de equipos que tienen menos de 4 GB de RAM. La nueva recopilación contendrá los equipos de escritorio de Dell que tengan al menos 4 GB de RAM.|  

 Use los procedimientos siguientes como ayuda para crear recopilaciones en Configuration Manager. También puede importar recopilaciones creadas en este u otro sitio de Configuration Manager. Para más información sobre cómo exportar recopilaciones, vea [Cómo administrar recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Para obtener información sobre la creación de recopilaciones para equipos que ejecutan Linux y UNIX, consulte [How to manage clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md) (Cómo administrar clientes para servidores Linux y UNIX en System Center Configuration Manager).  

##  <a name="BKMK_1"></a> Cómo crear una recopilación de dispositivos  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Recopilaciones de dispositivos**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear recopilación de dispositivos**.  

4.  En la página **General**, proporcione un **Nombre** y un **Comentario**. Después, en **Recopilación de restricción**, haga clic en **Examinar** para seleccionar una recopilación de restricción. La recopilación solo contendrá miembros de la recopilación de restricción.  

5.  En la página **Reglas de pertenencia** del **Asistente para crear recopilación de dispositivos**, en la lista **Agregar regla**, seleccione el tipo de regla de pertenencia que quiere usar para esta recopilación. Puede configurar varias reglas para cada recopilación.  

        
        ##### To configure a direct rule  

        1.  En la página **Buscar recursos** del **Asistente para crear reglas de pertenencia directa**, especifique la información siguiente:  

            -   **Clase de recurso**: seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso del sistema** para buscar datos de inventario devueltos de equipos cliente o **Equipo desconocido** para seleccionar entre los valores devueltos por equipos desconocidos.  

            -   **Nombre de atributo**: seleccione el atributo asociado a la clase de recurso seleccionado que quiere buscar. Por ejemplo, si quiere seleccionar equipos por su nombre NETBIOS, seleccione **Recurso del sistema** en la lista **Clase de recurso** y **Nombre NETBIOS** en la lista **Nombre de atributo** .  

            -   **Excluir recursos marcados como obsoletos**: si un equipo cliente está marcado como obsoleto, no incluya este valor en los resultados de la búsqueda.  

            -   **Excluir recursos que no tengan instalado el cliente de Configuration Manager**: estos no se mostrarán en los resultados de búsqueda.  

            -   **Valor:** escriba un valor por el que quiera buscar el nombre del atributo seleccionado. Puede utilizar el carácter de porcentaje **%** como carácter comodín. Por ejemplo, para buscar equipos que tengan un nombre NETBIOS que comience por "M", escriba **M%** en este campo.  

        2.  En la página **Seleccionar recursos**, seleccione los recursos que quiere agregar a la recopilación en la lista **Recursos** y luego haga clic en **Siguiente**.  


        ##### To configure a query rule  

        1.  En el cuadro de diálogo **Propiedades de regla de consulta** , especifique la siguiente información:  

            -   **Nombre**: especifique un nombre exclusivo.  

            -   **Importar instrucción de consulta**: abre el cuadro de diálogo **Examinar consulta** donde puede seleccionar una [consulta de Configuration Manager](../../../../core/servers/manage/create-queries.md) para usarla como la regla de consulta de la recopilación.   

            -   **Clase de recurso:** seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso del sistema** para buscar datos de inventario devueltos de equipos cliente o **Equipo desconocido** para seleccionar entre los valores devueltos por equipos desconocidos.  

            -   **Editar instrucción de consulta**: abre el cuadro de diálogo **Propiedades de instrucción de consulta** donde puede crear una consulta para usarla como regla de la recopilación. Para obtener más información sobre consultas, consulte [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Referencia técnica de consultas para System Center Configuration Manager).  

    
        ##### To configure an include collection rule  

        In the **Select Collections** dialog box, select the collections you want to include in the new collection, then choose **OK**.  

        ##### To configure an exclude collection rule  

        In the **Select Collections** dialog box, select the collections you want to exclude from the new collection, then choose **OK**.  

    -   **Usar actualizaciones incrementales para esta recopilación**: seleccione esta opción para detectar y examinar de forma periódica recursos nuevos o modificados con respecto a la evaluación de recopilación anterior, independientemente de que se realice una evaluación de recopilación completa. Las actualizaciones incrementales se producen en intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  Las recopilaciones configuradas mediante el uso de reglas que usan las clases siguientes no admiten las actualizaciones incrementales:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Programar una actualización completa en esta recopilación**: programe una evaluación completa regular de la pertenencia a la recopilación.  

6.  Complete el asistente para crear la nueva recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
>  Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación. Pero los miembros no aparecerán en la recopilación hasta después de la primera actualización programada o si selecciona manualmente **Actualizar pertenencia** para la recopilación. La actualización de colección puede tardar unos minutos en completarse.  

##  <a name="BKMK_2"></a> Cómo crear una recopilación de usuarios  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Usuarios de usuarios**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Crear recopilación de usuarios**.  

4.  En la página **General** del asistente, proporcione un **Nombre** y un **Comentario**. Después, en **Recopilación de restricción**, haga clic en **Examinar** para seleccionar una recopilación de restricción. La recopilación solo contendrá miembros de la recopilación de restricción.  

5.  En la página **Reglas de pertenencia**, especifique lo siguiente:  

    -   En la lista **Agregar regla** , seleccione el tipo de regla de pertenencia que quiere usar para esta recopilación. Puede configurar varias reglas para cada recopilación.  

         ##### <a name="to-configure-a-direct-rule"></a>Cómo configurar una regla directa  

        1.  En la página **Buscar recursos** del **Asistente para crear reglas de pertenencia directa**, especifique:  

            -   **Clase de recurso**: seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso de usuario** para buscar información de usuario recopilada por Configuration Manager o **Recurso de grupo de usuarios** para buscar información de grupo de usuarios recopilada por Configuration Manager.  

            -   **Nombre de atributo**: seleccione el atributo asociado a la clase de recurso que quiere buscar. Por ejemplo, si quiere seleccionar equipos por su nombre de unidad organizativa (UO), seleccione **Recurso de usuario** en la lista **Clase de recurso** y **Nombre de UO de usuario** en la lista **Nombre de atributo** .  

            -   **Valor:** escriba el valor por el que quiere buscar. Puede utilizar el carácter de porcentaje **%** como carácter comodín. Por ejemplo, para buscar usuarios en la UO de Contoso, escriba **Contoso** en este campo.  

        2.  En la página **Seleccionar recursos**, seleccione los recursos que quiere agregar a la recopilación en la lista **Recursos**.  

        ##### <a name="to-configure-a-query-rule"></a>Cómo configurar una regla de consulta  

        1.  En el cuadro de diálogo **Propiedades de regla de consulta**, proporcione lo siguiente:  

            -   **Nombre**: un nombre único.  

            -   **Importar instrucción de consulta**: abre el cuadro de diálogo **Examinar consulta** donde puede seleccionar una [consulta de Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) para usarla como la regla de consulta de la recopilación.  

            -   **Clase de recurso**: seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso de usuario** para buscar información de usuario recopilada por Configuration Manager o **Recurso de grupo de usuarios** para buscar información de grupo de usuarios recopilada por Configuration Manager.  

            -   **Editar instrucción de consulta**: abre el cuadro de diálogo **Propiedades de instrucción de consulta** donde puede [crear una consulta](../../../../core/servers/manage/queries-technical-reference.md) para usarla como regla para la recopilación.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Cómo configurar una regla de inclusión de recopilación  

        En el cuadro de diálogo **Seleccionar recopilaciones**, seleccione las recopilaciones que quiere incluir en la nueva recopilación y después pulse **Aceptar**.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Cómo configurar una regla de exclusión de recopilación  

        En el cuadro de diálogo **Seleccionar recopilaciones**, seleccione las recopilaciones que quiere excluir en la nueva recopilación y después pulse **Aceptar**.  


    -   **Usar actualizaciones incrementales para esta recopilación**: seleccione esta opción para detectar y examinar de forma periódica recursos nuevos o modificados con respecto a la evaluación de recopilación anterior, independientemente de que se realice una evaluación de recopilación completa. Las actualizaciones incrementales se producen en intervalos de 10 minutos.  

        > [!IMPORTANT]  
        >  Las recopilaciones configuradas mediante el uso de reglas que usan las clases siguientes no admiten las actualizaciones incrementales:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (solo para las recopilaciones de usuarios)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Programar una actualización completa en esta recopilación**: programe una evaluación completa regular de la pertenencia a la recopilación.  

6.  Complete el asistente. La nueva recopilación se muestra en el nodo **Recopilaciones de usuarios** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
>  Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación. Sin embargo, los miembros no aparecerán en la recopilación hasta después de la primera actualización programada o hasta que seleccione manualmente **Actualizar pertenencia** de la recopilación. La actualización de colección puede tardar unos minutos en completarse.  

##  <a name="BKMK_3"></a> Cómo importar una conexión  

1.  En la consola de Configuration Manager, seleccione **Activos y compatibilidad** > **Recopilaciones de usuarios** o **Recopilaciones de dispositivos**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, haga clic en **Importar recopilaciones**.  

4.  En la página **General** del **Asistente para importar recopilaciones**, haga clic en **Siguiente**.  

5.  En la página **Nombre de archivo MOF**, haga clic en **Examinar** y luego busque el archivo MOF que contenga la información de la recopilación que quiera importar.  

    > [!NOTE]  
    >  El archivo que quiera importar se debe haber exportado de un sitio que ejecute la misma versión de Configuration Manager que este. Para obtener más información sobre cómo exportar recopilaciones, consulte [How to manage collections in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md) (Cómo administrar recopilaciones en System Center Configuration Manager).  

6.  Complete el asistente para importar la recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** . Actualice o vuelva a cargar la consola de Configuration Manager para ver los miembros de la recopilación recién importada.  

