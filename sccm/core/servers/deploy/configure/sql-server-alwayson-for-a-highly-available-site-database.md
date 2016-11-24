---
title: SQL Server AlwaysOn | System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 570e651d486a6120eb062ef845930445596054da


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*



 A partir de la versión 1602 de System Center Configuration Manager, puede usar [grupos de disponibilidad AlwaysOn](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) de SQL Server para hospedar la base de datos de sitio en sitios primarios y el sitio de administración central como una solución de alta disponibilidad y recuperación ante desastres. El grupo de disponibilidad puede hospedarse de forma local o en Microsoft Azure.  

 Al utilizar Microsoft Azure para hospedar el grupo de disponibilidad, puede aumentar aún más la disponibilidad de la base de datos de sitio mediante el uso de grupos de disponibilidad AlwaysOn de SQL Server con conjuntos de disponibilidad de Azure. Para más información sobre los conjuntos de disponibilidad de Azure, consulte [Administrar la disponibilidad de las máquinas virtuales](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 Los siguientes son escenarios compatibles con grupos de disponibilidad:  

-   Puede mover la base de datos de sitio a la instancia predeterminada de un grupo de disponibilidad  

-   Puede agregar o quitar a miembros de la réplica de un grupo de disponibilidad que hospede una base de datos de sitio  

-   Puede mover la base de datos del sitio de un grupo de disponibilidad a una instancia predeterminado o designada de un servidor SQL Server independiente  


> [!NOTE]  
>  La configuración y el uso correctos de los grupos de disponibilidad requieren destreza en la configuración de grupos de disponibilidad de SQL Server y los grupos de disponibilidad de SQL Server. Los procedimientos para System Center Configuration Manager de este tema se basan en la documentación y los procedimientos adicionales que encontrará en la biblioteca de documentación de SQL Server.  

 **Problemas conocidos al usar grupos de disponibilidad AlwaysOn con Configuration Manager:**  

-   **Todos los servidores de réplica requieren una ruta de acceso idéntica al configurar Configuration Manager para utilizar el grupo de disponibilidad:**  

    -   En el momento de ejecutar el programa de instalación de Configuration Manager para redirigir el sitio para usar la base de datos en un grupo de disponibilidad, cada servidor de réplica secundario del grupo debe tener una ruta de acceso de archivo idéntica a la ruta de acceso usada para hospedar los archivos de base de datos del sitio en la réplica principal actual. Si no existe una ruta de acceso idéntica en las réplicas secundarias, se producirá un error en el programa de instalación al agregar la instancia de grupos de disponibilidad como nueva ubicación de la base de datos del sitio.  

         Además, en cada servidor de réplica secundaria, la cuenta de servicio de SQL Server local debe tener permiso de **Control total** para esta carpeta.  

         Los servidores de réplica secundaria solo requieren esta ruta de acceso de archivo mientras utilizan el programa de instalación para especificar la instancia de base de datos del grupo de disponibilidad.  Una vez que el programa de instalación completa el cambio para usar la base de datos de sitio en el grupo de disponibilidad, puede eliminar la ruta de acceso de los servidores de réplicas secundarias sin usar.  

         Por ejemplo, considere el siguiente escenario:  

        -   Crea un grupo de disponibilidad que utiliza tres servidores SQL Server  

        -   El servidor de réplica principal es una nueva instalación de SQL Server 2014.  De forma predeterminada, la base de datos. MDF y los archivos .LDF se almacenan en C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA  

        -   Dos de los servidores de réplica secundaria se actualizaron a SQL Server 2014 desde versiones anteriores y conservan la ruta del archivo original para almacenar los archivos de base de datos: C:\Program Files\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA  

        -   Antes de intentar mover la base de datos de sitio a este grupo de disponibilidad, en cada servidor de réplica secundaria debe crear la siguiente ruta de acceso, aunque las réplicas secundarias no utilicen esta ubicación de archivo: C:\Program Files\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA (un duplicado de la ruta de acceso que se usa en la réplica principal)  

        -   A continuación, concede a la cuenta de servicio de SQL Server de cada réplica secundaria control total de acceso a la ubicación del archivo recién creada en el servidor  

        -   Ahora puede ejecutar correctamente el programa de instalación de Configuration Manager para dirigir el sitio para usar la base de datos del grupo de disponibilidad  

-   **Al ejecutar el programa de instalación para dirigir la base de datos de sitio para utilizar el grupo de disponibilidad, se podrían registrar errores similares al siguiente en ConfigMgrSetup.log:**  

    -   ERROR: Error de SQL Server: [25000] [3906] [Microsoft] [SQL Server Native Client 11.0] [SQL Server] No se pudo actualizar la base de datos "CM_AAA" porque es de solo lectura.   Programa de instalación de Configuration Manager 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     Estos errores se registran cuando el programa de instalación intenta procesar roles de base de datos en réplicas secundarias del grupo de disponibilidad. Estos errores pueden omitirse sin problemas.
- **Servidores SQL Server que hospedan grupos de disponibilidad adicionales:**

  Antes de instalar la versión 1610, al usar un grupo de disponibilidad y después ejecutar el programa de instalación de Configuration Manager o instalar una actualización de Configuration Manager, cada réplica de cada grupo de disponibilidad adicional de SQL Server que hospeda el grupo de disponibilidad de Configuration Manager debe tener las siguientes configuraciones:
    - **conmutación por error manual**
    - **permitir cualquier conexión de solo lectura**


##  <a name="a-namebkmkbnra-changes-for-backup-and-recovery-when-you-use-a-sql-server-alwayson-availability-group"></a><a name="bkmk_BnR"></a> Cambios en Copia de seguridad y recuperación cuando se usa un grupo de disponibilidad AlwaysOn de SQL Server  
 **Copia de seguridad:**  

 Al ejecutar una base de datos de sitio en un grupo de disponibilidad, debe seguir ejecutando la tarea de mantenimiento del servidor del **sitio de copia de seguridad** integrada para realizar una copia de seguridad de los archivos y las configuraciones comunes de Configuration Manager, pero planee no usar los archivos .MDF o .LDF creados por esa copia de seguridad. Prevea en su lugar realizar copias de seguridad directas de la base de datos de sitio mediante SQL Server.  

 Además, dado que el modelo de recuperación de la base de datos está configurado en completa, debe planear la supervisión y el mantenimiento del tamaño del registro de transacciones de la base de datos de sitio.  En el modelo de recuperación completa, las transacciones no están protegidas hasta que se realiza una copia de seguridad completa de la base de datos o el registro de transacciones. El modelo de recuperación completa es un requisito para el uso de la base de datos de sitio en un grupo de disponibilidad y se establece al configurar el grupo para su uso con Configuration Manager. Para más información acerca de la copia de seguridad y restauración en SQL Server, consulte [Realizar copias de seguridad y restaurar bases de datos de SQL Server](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) en la documentación de SQL Server.  

 **Recuperación:**  

 Durante la recuperación del sitio, siempre y cuando un nodo del grupo de disponibilidad siga funcionando, podrá utilizar la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos de sitio permaneció intacta)**.  

 En cambio, si se han perdido todos los nodos de un grupo de disponibilidad, para poder recuperar el sitio debe volver a crear ese grupo de disponibilidad (System Center Configuration Manager no puede volver a generar o restaurar el nodo de disponibilidad).  Una vez que se haya vuelto a crear el grupo mediante la restauración y la reconfiguración de una copia de seguridad, podrá usar la opción de recuperación del sitio **Omitir recuperación de base de datos (use esta opción si la base de datos de sitio permaneció intacta)**.  

 Para obtener más información sobre la recuperación y copia de seguridad, consulte [Copia de seguridad y recuperación de System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="a-namebkmkcreatea-configure-an-availability-group-for-use-with-configuration-manager"></a><a name="bkmk_create"></a> Configuración de un grupo de disponibilidad para su uso con Configuration Manager  
 Antes de comenzar el siguiente procedimiento, familiarícese con los procedimientos de SQL Server necesarios para completar esta configuración y con los siguientes detalles que se aplican a los grupos de disponibilidad que configura para su uso con Configuration Manager.  

 **Requisitos para grupos de disponibilidad AlwaysOn que usa con System Center Configuration Manager:**  

-   Cada nodo (o réplica) del grupo de disponibilidad debe ejecutar una versión de SQL Server compatible con System Center Configuration Manager  

-   El grupo de disponibilidad debe tener una réplica principal y tener hasta dos réplicas secundarias sincrónicas.  

-  Después de agregar una base de datos a un grupo de disponibilidad, debe realizar una conmutación por error de la réplica principal a una secundaria (convirtiéndola en la nueva réplica principal) y configurar la base de datos con lo siguiente:
    - Habilitar Trustworthy: igual a True
    - Habilitar Service Broker: igual a True
    - Establecer dbowner: igual a SA

    Puede ejecutar el script siguiente para configurar estas opciones, donde cm_ABC es el nombre de la base de datos del sitio:  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647
    >     reconfigure



-   El grupo de disponibilidad debe tener al menos un **agente de escucha de grupo de disponibilidad**.  El nombre virtual de este agente de escucha se usa al configurar Configuration Manager para usar la base de datos de sitio en el grupo de disponibilidad. Aunque un grupo de disponibilidad puede contener varios agentes de escucha, Configuration Manager solo puede usar uno  

-   Cada réplica principal y secundaria debe:  
    - Establecerse para **permitir cualquier conexión de solo lectura**
    - Utilizar la **instancia predeterminada**
    - Establecerse para la **conmutación por error manual**  

        > [!TIP]  
        >  System Center Configuration Manager admite el uso de las réplicas del grupo de disponibilidad cuando se establece en conmutación automática por error. En cambio, debe establecerse la conmutación por error manual al ejecutar el programa de instalación para especificar el uso de la base de datos de sitio en el grupo de disponibilidad y en el momento de instalar las actualizaciones de Configuration Manager (no solo las actualizaciones que se aplican a la base de datos de sitio).  

  **Limitaciones de los grupos de disponibilidad**
   - Los grupos de disponibilidad solo son compatibles con la base de datos del sitio y no para la de actualización de software ni de informes.   
   - Al usar un grupo de disponibilidad debe configurar manualmente el punto de notificación para que use la réplica principal actual y no el agente de escucha del grupo de disponibilidad. Si la réplica principal conmuta por error a otra réplica, a continuación, debe volver a configurar el punto de notificación para que use la nueva réplica principal.  
   - Antes de instalar las actualizaciones, como en la versión 1606, asegúrese de que el grupo de disponibilidad está establecido para la conmutación por error manual. Después de que se actualice el sitio, puede restaurar la conmutación por error a automática.



 **Permisos necesarios para configurar y usar grupos de disponibilidad:**  

-   La cuenta de equipo del servidor del sitio debe formar parte del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>Para configurar un grupo de disponibilidad para hospedar una base de datos de sitio  

1.  Use el siguiente comando para detener el sitio de Configuration Manager:  
     **Preinst.exe /stopsite**  

     Para obtener más información sobre el uso de Preinst.exe, consulte [Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Cambie el modelo de copia de seguridad de la base de datos de sitio de **SENCILLA** a **COMPLETA**.  

     Consulte [Ver o cambiar el modelo de recuperación de una base de datos (SQL Server)](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) en la documentación de SQL Server. (Los grupos de disponibilidad solo admiten COMPLETA).  

3.  Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio y, a continuación:  

    -   Si el servidor de la base de datos de sitio actual no será miembro del grupo de disponibilidad o no se utilizará como réplica principal inicial del grupo de disponibilidad, restaure una copia de la base de datos de sitio en el servidor que hospedará la réplica principal del grupo.  

    -   Si el servidor de la base de datos de sitio actual será miembro del grupo de disponibilidad, planee el uso de este servidor como miembro de la réplica principal del grupo de disponibilidad. Cuando lo haga, no tendrá que restaurar una copia de la base de datos de sitio a este u otro servidor.  

    Para obtener información sobre cómo completar este paso, consulte [Crear una copia de seguridad completa de base de datos (SQL Server)](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) y [Restaurar una copia de seguridad de base de datos (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx)en la documentación de SQL Server.  

4.  En el servidor que hospedará la réplica principal del grupo, use el **Asistente para nuevo grupo de disponibilidad** para crear el grupo de disponibilidad. En el asistente:  

    -   En la página **Seleccionar base de datos**, seleccione la base de datos para el sitio de Configuration Manager  

    -   En la página **Especificar réplicas** , configure lo siguiente:  

        -   **Réplicas**: especifique los servidores que hospedarán las réplicas secundarias.  

        -   **Agente de escucha**: especifique el **Nombre DNS del agente de escucha** como un nombre DNS completo, como **&lt;servidor_agente_escucha>.fabrikam.com**. Esto sirve al configurar Configuration Manager para usar la base de datos de sitio en el grupo de disponibilidad.

    -   En la página **Seleccionar sincronización de datos iniciales** seleccione **Completa**. Una vez que el asistente cree el grupo de disponibilidad, hará una copia de seguridad del registro de transacciones y la base de datos principal y los restaurará en cada servidor que hospede una réplica secundaria. Si no sigue este paso, tendrá que restaurar una copia de la base de datos de sitio en cada servidor que hospeda una réplica secundaria y unir manualmente esa base de datos al grupo.  

    Para más información, consulte [Usar el Asistente para grupo de disponibilidad (SQL Server Management Studio)](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) en la documentación de SQL Server.  

5.  Una vez configurado el grupo de disponibilidad, configure la base de datos de sitio en la réplica principal con la propiedad **TRUSTWORTHY** y **habilite la integración CLR**. Para obtener información acerca de cómo realizar estas configuraciones, consulte [Propiedad de base de datos TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) y  [Habilitar la integración CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) en la documentación de SQL Server.  

6.  Realice las acciones siguientes para configurar cada réplica secundaria en el grupo de disponibilidad:  

    1.  Realice una conmutación por error manual de la réplica principal actual en una réplica secundaria. Consulte [Realizar una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) en la documentación de SQL Server.  

    2.  Configure la base de datos en la nueva réplica principal con la propiedad **TRUSTWORTHY** y **habilite la integración CLR**.  

7.  Una vez que todas las réplicas hayan ascendido a réplicas principales y se hayan configurado las bases de datos, el grupo de disponibilidad estará listo para su uso con Configuration Manager.  





##  <a name="a-namebkmkdirecta-move-a-site-database-to-an-availability-group"></a><a name="bkmk_direct"></a> Traslado de una base de datos de sitio a un grupo de disponibilidad  
 Puede mover una base de datos de sitio de un sitio de instalación anterior a un grupo de disponibilidad. Primero debe crear el grupo de disponibilidad y, a continuación, configurar la base de datos para que funcione en el grupo de disponibilidad.  

 Para completar este procedimiento, la cuenta de usuario que ejecuta el programa de instalación de Configuration Manager debe ser miembro del grupo de **administradores locales** de cada equipo que sea miembro del grupo de disponibilidad.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>Para mover una base de datos de sitio a un grupo de disponibilidad  

1.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;carpeta de instalación del sitio de Configuration Manager\>\BIN\X64\setup.exe**.  

2.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

3.  A continuación, seleccione la opción **Modificar configuración de SQL Server** y luego haga clic en **Siguiente**.  

4.  Vuelva a configurar lo siguiente en la base de datos de sitio:  

    -   **Nombre de SQL Server** : escriba el nombre virtual para el agente de escucha que configuró al crear el grupo de disponibilidad. El nombre virtual debe ser un nombre DNS completo, como **&lt;endpointServer\>. fabrikam.com**  

    -   **Instancia** : este valor debe estar en blanco para especificar la instancia predeterminada para el agente de escucha del grupo de disponibilidad.  Si la base de datos de sitio actual está instalada en una instancia con nombre, esta aparecerá y debe borrarse.  

    -   **Base de datos** : deje el nombre tal y como aparece. Este es el nombre de la base de datos de sitio actual.  

5.  Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales.  

##  <a name="a-namebkmkchangea-add-or-remove-members-of-an-active-availability-group"></a><a name="bkmk_change"></a> Adición o eliminación de miembros de un grupo de disponibilidad activo  
 Después de que Configuration Manager use una base de datos de sitio hospedada en un grupo de disponibilidad, puede quitar un miembro de la réplica o agregar un miembro de la réplica adicional (sin superar un nodo principal y dos secundarios).  

#### <a name="to-add-a-new-replica-member"></a>Para agregar un nuevo miembro de réplica  

1.  Agregue el nuevo servidor como réplica secundaria al grupo de disponibilidad. Consulte  [Agregar una réplica secundaria a un grupo de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)en la biblioteca de documentación de SQL Server.  

2.  Detenga el sitio de Configuration Manager al ejecutar **Preinst.exe /stopsite**. Consulte [Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

3.  Use SQL Server para crear una copia de seguridad de la base de datos de sitio de la réplica principal y, a continuación, restaure esa copia en el nuevo servidor de réplica secundaria. Consulte [Crear una copia de seguridad completa de base de datos (SQL Server)](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) y [Restaurar una copia de seguridad de base de datos (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) en la biblioteca de documentación de SQL Server.  

4.  Configure cada réplica secundaria. Realice las siguientes acciones para cada réplica secundaria del grupo de disponibilidad:  

    1.  Realice una conmutación por error manual de la réplica principal en la nueva réplica secundaria. Consulte [Realizar una conmutación por error manual planeada de un grupo de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) en la documentación de SQL Server.  

    2.  Configure la base de datos en el nuevo servidor para que sea de confianza y habilite la integración CLR. Consulte [Propiedad de base de datos TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) y  [Habilitar la integración CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)en la documentación de SQL Server.  

5.  Reinicie el sitio iniciando los servicios Administrador de componentes de sitio (**sitecomp**) y **SMS_Executive** .  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>Para quitar un miembro de la réplica del grupo de disponibilidad  

-   Utilice la información de [Quitar una réplica secundaria de un grupo de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) en la documentación de SQL Server.  

##  <a name="a-namebkmkremovea-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a><a name="bkmk_remove"></a> Traslado de la base de datos de sitio desde un grupo de disponibilidad de nuevo a una sola instancia de SQL Server  
 Utilice el procedimiento siguiente cuando ya no desee hospedar la base de datos de sitio en un grupo de disponibilidad.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Para mover la base de datos de sitio desde un grupo de disponibilidad de nuevo a una sola instancia de SQL Server  

1.  Para detener el sitio de Configuration Manager, use el siguiente comando:  
     **Preinst.exe /stopsite**.  Para obtener más información, consulte [Herramienta de mantenimiento de jerarquía (Preinst.exe) para System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Use SQL Server para crear una copia de seguridad completa de la base de datos de sitio desde la réplica principal. Para obtener información sobre cómo completar este paso, consulte [Crear una copia de seguridad completa de base de datos (SQL Server)](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) en la documentación de SQL Server.  

3.  Si el servidor que hospeda la réplica principal del grupo de disponibilidad hospedará ahora la instancia sencilla de la base de datos de sitio, puede omitir este paso:  

    -   Utilice SQL Server para restaurar la copia de seguridad de la base de datos de sitio en el servidor que hospedará la base de datos de sitio.  Consulte [Restaurar una copia de seguridad de base de datos (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) en la documentación de SQL Server.  

4.  En la base de datos de sitio restaurada, cambie el modelo de copia de seguridad de la base de datos de sitio de **COMPLETA** a **SENCILLA**.  Consulte [Ver o cambiar el modelo de recuperación de una base de datos (SQL Server)](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) en la documentación de SQL Server.  

5.  Ejecute el **programa de instalación de Configuration Manager** desde la **&lt;carpeta de instalación del sitio de Configuration Manager\>\BIN\X64\setup.exe**.  

6.  En la página **Primeros pasos** , seleccione **Realizar mantenimiento de sitio o restablecer este sitio**y, a continuación, haga clic en **Siguiente**.  

7.  A continuación, seleccione la opción **Modificar configuración de SQL Server** y luego haga clic en **Siguiente**.  

8.  Vuelva a configurar lo siguiente en la base de datos de sitio:  

    -   **Nombre de SQL Server** : escriba el nombre del servidor que hospeda ahora la base de datos de sitio.  

    -   **Instancia** : especifique la instancia designada que hospeda la base de datos o deje este campo en blanco si la base de datos se encuentra en la instancia predeterminada.  

    -   **Base de datos** : deje el nombre tal y como aparece. Este es el nombre de la base de datos de sitio actual.  

9. Después de proporcionar la información de la nueva ubicación de la base de datos, complete el programa de instalación con los procesos y las configuraciones habituales. Cuando finalice la instalación, el sitio se reinicia y comienza a utilizar la nueva ubicación de la base de datos.  

10. Para limpiar los servidores que eran miembros del grupo de disponibilidad, siga las instrucciones de [Quitar un grupo de disponibilidad (SQL Server)](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) en la documentación de SQL Server.



<!--HONumber=Nov16_HO1-->


