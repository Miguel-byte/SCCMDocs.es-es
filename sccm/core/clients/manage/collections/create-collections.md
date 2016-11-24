---
title: Crear recopilaciones | System Center Configuration Manager
description: "Cree recopilaciones en System Center Configuration Manager para facilitar la administración de grupos de usuarios y dispositivos."
ms.custom: na
ms.date: 10/06/2016
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
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f73f0e58b82d1aab1f64f3695dd5c3a61e933d2a


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Cómo crear recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Cree recopilaciones en System Center Configuration Manager para representar agrupaciones lógicas de usuarios o dispositivos. Puede utilizar las recopilaciones como ayuda para realizar muchas tareas, incluida la administración de aplicaciones, la implementación de la configuración de cumplimiento o la instalación de actualizaciones de software. También puede utilizar las recopilaciones para administrar grupos de configuraciones de cliente o usarlas con administración basada en roles para especificar recursos a los que puede un usuario administrativo puede acceder. Configuration Manager contiene varias recopilaciones integradas. Para obtener más información, consulte [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md) (Introducción a las recopilaciones en System Center Configuration Manager).  

> [!NOTE]  
>  Una recopilación única puede contener o bien usuarios o bien dispositivos, pero no ambos.  

 En la tabla siguiente, se enumeran las reglas que puede usar para configurar los miembros de una recopilación en Configuration Manager.  

|Tipo de regla de pertenencia|Más información|  
|--------------------------|----------------------|  
|Regla directa|Las reglas directas permiten elegir los usuarios o equipos que quiera agregar como miembros a una recopilación. Esta regla ofrece control directo sobre qué recursos son miembros de la recopilación. Esta pertenencia no cambia a menos que se quite un recurso de Configuration Manager. Configuration Manager debe haber detectado los recursos o se deben haber importado los recursos antes de poderlos agregar a una recopilación de regla directa. Las recopilaciones de reglas directas tienen una mayor carga administrativa que recopilaciones de reglas de consulta, ya que debe realizar los cambios en este tipo de recopilación de forma manual.|  
|Regla de consulta|Las reglas de consulta actualizan de forma dinámica la pertenencia de una recopilación basándose en una consulta que Configuration Manager ejecuta según una programación. Por ejemplo, puede crear una recopilación de usuarios que sean miembros de la unidad organizativa Recursos humanos de los Servicios de dominio de Active Directory. A diferencia de las recopilaciones de reglas directas, esta pertenencia a la recopilación se actualiza automáticamente cuando se agregan usuarios nuevos o se quitan usuarios de la unidad organizativa Recursos humanos.<br /><br /> Para obtener consultas de ejemplo que puede usar para crear recopilaciones, consulte [How to create queries in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md) (Cómo crear consultas en System Center Configuration Manager).|  
|Regla de inclusión de recopilación|La regla de inclusión de recopilación permite incluir los miembros de otra recopilación en una recopilación de Configuration Manager. La pertenencia de la recopilación actual se actualiza según una programación si la pertenencia de la recopilación incluida ha cambiado.<br /><br /> Puede agregar varias reglas de inclusión de recopilación a una recopilación.<br />              **Ejemplo:** se crea una recopilación que tiene dos reglas de inclusión de recopilación. La primera regla de inclusión de recopilación es para una recopilación de portátiles y la segunda regla de inclusión de recopilación es para una recopilación de equipos de escritorio. La nueva recopilación contendrá a todos los miembros de la recopilación de portátiles y de la recopilación de equipos de escritorio.|  
|Regla de exclusión de recopilación|La regla de exclusión de recopilación le permite excluir los miembros de otra recopilación de una recopilación de Configuration Manager. La pertenencia de la recopilación actual se actualiza según una programación si la pertenencia de la recopilación excluida ha cambiado.<br /><br /> Puede agregar varias reglas de exclusión de recopilación a una recopilación. Si una recopilación incluye tanto reglas de inclusión de recopilación como reglas de exclusión de recopilación y se produce un conflicto, la regla de exclusión de recopilación tiene prioridad sobre la regla de inclusión de recopilación.<br />              **Ejemplo:** se crea una recopilación que tiene una regla de inclusión de recopilación y una regla de exclusión de recopilación. La regla de inclusión de recopilación es para una recopilación de equipos de escritorio de Dell. La de exclusión de recopilación es una recopilación de equipos que tienen menos de 4 GB de RAM. La nueva recopilación contendrá los equipos de escritorio de Dell que tengan al menos 4 GB de RAM.|  

 Use los procedimientos siguientes como ayuda para crear recopilaciones en Configuration Manager. También puede importar recopilaciones creadas en este u otro sitio de Configuration Manager. Para obtener información sobre cómo exportar recopilaciones, consulte [How to manage collections in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md) (Cómo administrar recopilaciones en System Center Configuration Manager).  

 Para obtener información sobre la creación de recopilaciones para equipos que ejecutan Linux y UNIX, consulte [How to manage clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md) (Cómo administrar clientes para servidores Linux y UNIX en System Center Configuration Manager).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> Cómo crear una recopilación de dispositivos  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de dispositivos**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear recopilación de dispositivos**.  

4.  En la página **General** del **Asistente para crear recopilación de dispositivos**, especifique la información siguiente:  

    -   **Nombre**: especifique un nombre único para la recopilación.  

    -   **Comentario**: especifique una descripción para la recopilación.  

    -   **Recopilación de restricción**: haga clic en **Examinar** para seleccionar una recopilación de restricción. La recopilación que está creando solo contendrá miembros de la recopilación de restricción.  

5.  En la página **Reglas de pertenencia** del **Asistente para crear recopilación de dispositivos**, especifique la información siguiente:  

    -   En la lista **Agregar regla** , seleccione el tipo de regla de pertenencia que quiere usar para esta recopilación. Puede configurar varias reglas para cada recopilación.  

         Utilice los procedimientos siguientes para configurar cada tipo de regla de pertenencia.  

        ##### <a name="to-configure-a-direct-rule"></a>Cómo configurar una regla directa  

        1.  En la página **Buscar recursos** del **Asistente para crear reglas de pertenencia directa**, especifique la información siguiente:  

            -   **Clase de recurso**: en la lista, seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso del sistema** para buscar datos de inventario devueltos de equipos cliente o **Equipo desconocido** para seleccionar entre los valores devueltos por equipos desconocidos.  

            -   **Nombre de atributo**: en la lista, seleccione el atributo asociado a la clase de recurso seleccionado que quiere buscar. Por ejemplo, si quiere seleccionar equipos por su nombre NETBIOS, seleccione **Recurso del sistema** en la lista **Clase de recurso** y **Nombre NETBIOS** en la lista **Nombre de atributo** .  

            -   **Excluir recursos marcados como obsoletos**: si un equipo cliente está marcado como obsoleto, no incluya este valor en los resultados de la búsqueda.  

            -   **Excluir recursos que no tengan instalado el cliente de Configuration Manager**: si los resultados de la búsqueda incluyen un recurso que no tiene un cliente de Configuration Manager instalado, este valor no se mostrará en los resultados de la búsqueda.  

            -   **Valor:** escriba un valor por el que quiera buscar el nombre del atributo seleccionado. Puede utilizar el carácter de porcentaje **%** como carácter comodín. Por ejemplo, si quiere buscar equipos que tengan un nombre NETBIOS que comience por "M", escriba **M%** en este campo.  

        2.  En la página **Seleccionar recursos** del **Asistente para crear reglas de pertenencia directa**, seleccione los recursos que quiere agregar a la recopilación en la lista **Recursos** y luego haga clic en **Siguiente**.  

        3.  Complete el **Asistente para crear reglas de pertenencia directa**.  

        ##### <a name="to-configure-a-query-rule"></a>Cómo configurar una regla de consulta  

        1.  En el cuadro de diálogo **Propiedades de regla de consulta** , especifique la siguiente información:  

            -   **Nombre**: especifique un nombre único para la regla de consulta.  

            -   **Importar instrucción de consulta**: abre el cuadro de diálogo **Examinar consulta** donde puede seleccionar una consulta de Configuration Manager para usarla como la regla de consulta de la recopilación. Para obtener más información sobre cómo crear estas consultas y algunos ejemplos, consulte [How to create queries in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md) (Cómo crear consultas en System Center Configuration Manager).  

            -   **Clase de recurso** : en la lista, seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso del sistema** para buscar datos de inventario devueltos de equipos cliente o **Equipo desconocido** para seleccionar entre los valores devueltos por equipos desconocidos.  

            -   **Editar instrucción de consulta**: abre el cuadro de diálogo **Propiedades de instrucción de consulta** donde puede crear una consulta para usarla como regla de la recopilación. Para obtener más información sobre consultas, consulte [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Referencia técnica de consultas para System Center Configuration Manager).  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de regla de consulta** y guardar la regla de pertenencia de la consulta.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Cómo configurar una regla de inclusión de recopilación  

        1.  En el cuadro de diálogo **Seleccionar recopilaciones** , seleccione las recopilaciones que quiere incluir en la nueva recopilación.  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar recopilaciones** y guardar la regla de inclusión de recopilación.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Cómo configurar una regla de exclusión de recopilación  

        1.  En el cuadro de diálogo **Seleccionar recopilaciones** , seleccione las recopilaciones que quiere excluir de la nueva recopilación.  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar recopilaciones** y guardar la regla de exclusión de recopilación.  

    -   **Usar actualizaciones incrementales para esta recopilación**: seleccione esta opción para detectar de forma periódica recursos nuevos o modificados con respecto a la evaluación de recopilación anterior y actualizar la pertenencia a la recopilación solo con estos recursos, independientemente de que se realice una evaluación de recopilación completa. Las actualizaciones incrementales se producen en intervalos de 10 minutos.  

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

    -   **Programar una actualización completa en esta recopilación**: seleccione esta opción para programar una evaluación completa regular de la pertenencia a la recopilación.  

6.  Complete el asistente para crear la nueva recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
>  Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación. Sin embargo, los miembros no aparecerán en la recopilación hasta después de la primera actualización programada o hasta que seleccione manualmente **Actualizar pertenencia** de la recopilación. Según la complejidad de la regla de recopilación y el número de entradas de la base de datos de Configuration Manager, pueden pasar unos minutos hasta que se complete una actualización de recopilación.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> Cómo crear una recopilación de usuarios  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de usuarios**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear recopilación de usuarios**.  

4.  En la página **General** del **Asistente para crear recopilación de usuarios**, especifique la información siguiente:  

    -   **Nombre**: especifique un nombre único para la recopilación.  

    -   **Comentario**: especifique una descripción para la recopilación.  

    -   **Recopilación de restricción**: haga clic en **Examinar** para seleccionar una recopilación de restricción. La recopilación que está creando solo contendrá miembros de la recopilación de restricción.  

5.  En la página **Reglas de pertenencia** del **Asistente para crear recopilación de usuarios**, especifique la información siguiente:  

    -   En la lista **Agregar regla** , seleccione el tipo de regla de pertenencia que quiere usar para esta recopilación. Puede configurar varias reglas para cada recopilación.  

         Utilice los procedimientos siguientes para configurar cada tipo de regla de pertenencia.  

        ##### <a name="to-configure-a-direct-rule"></a>Cómo configurar una regla directa  

        1.  En la página **Buscar recursos** del **Asistente para crear reglas de pertenencia directa**, especifique la información siguiente:  

            -   **Clase de recurso**: en la lista, seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso de usuario** para buscar información de usuario recopilada por Configuration Manager o **Recurso de grupo de usuarios** para buscar información de grupo de usuarios recopilada por Configuration Manager.  

            -   **Nombre de atributo**: en la lista, seleccione el atributo asociado a la clase de recurso seleccionado que quiere buscar. Por ejemplo, si quiere seleccionar equipos por su nombre de unidad organizativa (UO), seleccione **Recurso de usuario** en la lista **Clase de recurso** y **Nombre de UO de usuario** en la lista **Nombre de atributo** .  

            -   **Valor:** escriba un valor por el que quiera buscar el nombre del atributo seleccionado. Puede utilizar el carácter de porcentaje **%** como carácter comodín. Por ejemplo, si quisiera buscar usuarios en la UO de Contoso, escriba **Contoso** en este campo.  

        2.  En la página **Seleccionar recursos** del **Asistente para crear reglas de pertenencia directa**, seleccione los recursos que quiere agregar a la recopilación en la lista **Recursos** y luego haga clic en **Siguiente**.  

        3.  Complete el **Asistente para crear reglas de pertenencia directa**.  

        ##### <a name="to-configure-a-query-rule"></a>Cómo configurar una regla de consulta  

        1.  En el cuadro de diálogo **Propiedades de regla de consulta** , especifique la siguiente información:  

            -   **Nombre**: especifique un nombre único para la regla de consulta.  

            -   **Importar instrucción de consulta**: abre el cuadro de diálogo **Examinar consulta** donde puede seleccionar una consulta de Configuration Manager para usarla como la regla de consulta de la recopilación. Para obtener más información sobre consultas, consulte [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Referencia técnica de consultas para System Center Configuration Manager).  

            -   **Clase de recurso**: en la lista, seleccione el tipo de recurso que quiere buscar y agregar a la recopilación. Seleccione uno de los valores de **Recurso de usuario** para buscar información de usuario recopilada por Configuration Manager o **Recurso de grupo de usuarios** para buscar información de grupo de usuarios recopilada por Configuration Manager.  

            -   **Editar instrucción de consulta**: abre el cuadro de diálogo **Propiedades de instrucción de consulta** donde puede crear una consulta para usarla como regla de la recopilación. Para obtener más información sobre consultas, consulte [Queries technical reference for System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) (Referencia técnica de consultas para System Center Configuration Manager).  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de regla de consulta** y guardar la regla de pertenencia de la consulta.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Cómo configurar una regla de inclusión de recopilación  

        1.  En el cuadro de diálogo **Seleccionar recopilaciones** , seleccione las recopilaciones que quiere incluir en la nueva recopilación.  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar recopilaciones** y guardar la regla de inclusión de recopilación.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Cómo configurar una regla de exclusión de recopilación  

        1.  En el cuadro de diálogo **Seleccionar recopilaciones** , seleccione las recopilaciones que quiere excluir de la nueva recopilación.  

        2.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar recopilaciones** y guardar la regla de exclusión de recopilación.  

    -   **Usar actualizaciones incrementales para esta recopilación**: seleccione esta opción para detectar de forma periódica recursos nuevos o modificados con respecto a la evaluación de recopilación anterior y actualizar la pertenencia a la recopilación solo con estos recursos, independientemente de que se realice una evaluación de recopilación completa. Las actualizaciones incrementales se producen en intervalos de 10 minutos.  

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

    -   **Programar una actualización completa en esta recopilación**: seleccione esta opción para programar una evaluación completa regular de la pertenencia a la recopilación.  

6.  Complete el asistente para crear la nueva recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de usuarios** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
>  Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación. Sin embargo, los miembros no aparecerán en la recopilación hasta después de la primera actualización programada o hasta que seleccione manualmente **Actualizar pertenencia** de la recopilación. Según la complejidad de la regla de recopilación y el número de entradas de la base de datos de Configuration Manager, pueden pasar unos minutos hasta que se complete una actualización de recopilación.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> Cómo importar una conexión  

1.  En la consola de Configuration Manager, haga clic en **Activos y compatibilidad**.  

2.  En el área de trabajo **Activos y compatibilidad** , haga clic en **Recopilaciones de usuarios** o en **Recopilaciones de dispositivos**.  

3.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Importar recopilaciones**.  

4.  En la página **General** del **Asistente para importar recopilaciones**, haga clic en **Siguiente**.  

5.  En la página **Nombre de archivo MOF** , haga clic en **Examinar** y luego busque el archivo MOF que contenga la información de la recopilación que quiera importar.  

    > [!NOTE]  
    >  El archivo que quiera importar se debe haber exportado de un sitio que ejecute la misma versión de Configuration Manager que este. Para obtener más información sobre cómo exportar recopilaciones, consulte [How to manage collections in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md) (Cómo administrar recopilaciones en System Center Configuration Manager).  

6.  Complete el asistente para importar la recopilación. La nueva recopilación se muestra en el nodo **Recopilaciones de usuarios** o **Recopilaciones de dispositivos** del área de trabajo **Activos y compatibilidad** .  

> [!NOTE]  
>  Debe actualizar o volver a cargar la consola de Configuration Manager para ver los miembros de la recopilación recién importada.  



<!--HONumber=Nov16_HO1-->


