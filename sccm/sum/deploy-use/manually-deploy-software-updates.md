---
title: Implementar actualizaciones de software manualmente
titleSuffix: Configuration Manager
description: "Para implementar actualizaciones manualmente, seleccione actualizaciones en la consola de Configuration Manager e impleméntelas manualmente, o agregue actualizaciones a un grupo de actualizaciones e implemente el grupo."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: becab57c5f04bb67512d665175038f6c477b65b1
ms.sourcegitcommit: e13bb2c86c40a88e5f4602beb1d31e4adc90e099
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
#  <a name="BKMK_ManualDeploy"></a> Implementar actualizaciones de software manualmente  

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Una implementación de actualizaciones de software manual es el proceso de selección de actualizaciones de software desde la consola de Configuration Manager e inicio manual del proceso de implementación. También, se pueden agregar actualizaciones de software seleccionadas a un grupo de actualización para, a continuación, implementar manualmente el grupo de actualización. La implementación manual se suele usar para actualizar los dispositivos cliente con las actualizaciones de software necesarias para, posteriormente, crear reglas de implementación automática (ADR) que administren las implementaciones de actualizaciones de software mensuales. También se utiliza un método manual para implementar actualizaciones de software fuera de banda. Si necesita ayuda para determinar qué método de implementación es el adecuado para usted, vea [Deploy software updates](deploy-software-updates.md) (Implementación de actualizaciones de software).

 Las secciones siguientes proporcionan los pasos para implementar manualmente las actualizaciones de software.  

##  <a name="BKMK_1SearchCriteria"></a> Paso 1: especificar criterios de búsqueda para las actualizaciones de software  
 La consola de Configuration Manager puede incluir miles de actualizaciones de software. El primer paso del flujo de trabajo para implementar manualmente las actualizaciones de software es identificar aquéllas que desea implementar. Por ejemplo, podría especificar criterios para la recuperación de todas las actualizaciones de software que se requieran en más de 50 dispositivos cliente, y que tengan una clasificación de actualización de software de **Seguridad** o **Crítica** .  

> [!IMPORTANT]  
>  En una implementación de actualizaciones de software se pueden incluir hasta 1000 actualizaciones de software.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>Para especificar criterios de búsqueda de actualizaciones de software  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo de la biblioteca de software, expanda **Actualizaciones de software**y haga clic en **Todas las actualizaciones de software**. Se muestran las actualizaciones de software sincronizadas.  

    > [!NOTE]  
    >  En el nodo **Todas las actualizaciones de software** solo se muestran actualizaciones de software con una clasificación de **Crítica** y **Seguridad** publicadas en los últimos 30 días.  

3.  En el panel de búsqueda, complete uno de los siguientes pasos, o ambos, para filtrar e identificar las actualizaciones de software que necesita:  

    -   En el cuadro de texto de búsqueda, escriba una cadena de búsqueda que filtre las actualizaciones de software. Por ejemplo, escriba el identificador de artículo o el identificador de boletín de una actualización de software específica, o escriba una cadena que pudiera aparecer en el título de varias actualizaciones de software.  

    -   Haga clic en **Agregar criterios**, seleccione los criterios que va a utilizar para filtrar las actualizaciones de software, haga clic en **Agregar**y, a continuación, especifique los valores para los criterios.  

4.  Haga clic en **Buscar** para filtrar las actualizaciones de software.  

    > [!TIP]  
    >  Puede guardar los criterios del filtro en la pestaña **Buscar** , en el grupo **Guardar** .  

##  <a name="BKMK_2UpdateGroup"></a> Paso 2: crear un grupo de actualizaciones de software que contenga las actualizaciones de software  
 Los grupos de actualizaciones de software suponen un método eficaz para organizar las actualizaciones de software necesarias para la posterior implementación. Puede agregar manualmente actualizaciones de software a un grupo de actualizaciones de software, o bien Configuration Manager puede agregarlas automáticamente a un grupo de actualizaciones de software nuevo o existente, mediante una regla de implementación automática (ADR). Utilice los siguientes procedimientos para agregar manualmente actualizaciones de software a un grupo de actualizaciones de software nuevo.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>Para agregar manualmente las actualizaciones de software a un grupo de actualizaciones de software nuevo  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo de la biblioteca de software, haga clic en **Actualizaciones de software**.  

3.  Seleccione las actualizaciones de software que se van a agregar al grupo de actualizaciones de software nuevo.  

4.  En la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Crear grupo de actualizaciones de software**.  

5.  Especifique el nombre para el grupo de actualizaciones de software y, opcionalmente, incluya una descripción. Utilice un nombre y una descripción que proporcione información suficiente para determinar qué tipo de actualizaciones de software incluye el grupo de actualizaciones de software. Para proceder, haga clic en **Crear**.  

6.  Haga clic en el nodo **Grupos de actualizaciones de software** para mostrar el grupo de actualizaciones de software nuevo.  

7.  Seleccione el grupo de actualizaciones de software y, en la pestaña **Inicio** , en el grupo **Actualizar** , haga clic en **Mostrar miembros** para mostrar una lista de las actualizaciones de software incluidas en el grupo.  

##  <a name="BKMK_3DownloadContent"></a> Paso 3: descargar el contenido para el grupo de actualizaciones de software  
 Si lo desea, antes de implementar las actualizaciones de software, puede descargar el contenido para las actualizaciones incluidas en el grupo de actualizaciones de software. Esta opción es conveniente para poder comprobar la disponibilidad del contenido en los puntos de distribución antes de implementar las actualizaciones de software. Se evitarán así problemas inesperados con la entrega de contenido. Este paso se puede omitir para que el contenido se descargue y copie en los puntos de distribución como parte del proceso de implementación. Utilice el siguiente procedimiento para descargar el contenido para las actualizaciones de software del grupo de actualizaciones de software.  



#### <a name="to-download-content-for-the-software-update-group"></a>Para descargar el contenido para el grupo de actualizaciones de software
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>Para supervisar el estado del contenido
1. Para supervisar el estado del contenido para las actualizaciones de software, haga clic en **Supervisión** en la consola de Configuration Manager.  

2. En el área de trabajo Supervisión, expanda **Estado de distribución**y, a continuación, haga clic en **Estado de contenido**.  

3. Seleccione el paquete de actualizaciones de software que identificó previamente para descargar las actualizaciones de software en el grupo de actualizaciones de software.  

4. En la pestaña **Inicio** , en el grupo **Contenido** , haga clic en **Ver estado**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Paso 4: implementar el grupo de actualizaciones de software  
 Tras determinar las actualizaciones de software que quiere implementar y agregar estas actualizaciones a un grupo de actualizaciones de software, puede implementar manualmente las actualizaciones de software en el grupo de actualizaciones de software. Utilice el siguiente procedimiento para implementar manualmente las actualizaciones de software en un grupo de actualizaciones de software.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Para implementar manualmente las actualizaciones de software en un grupo de actualizaciones de software  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software**.  

2.  En el área de trabajo de la biblioteca de software, expanda **Actualizaciones de software**y haga clic en **Grupos de actualizaciones de software**.  

3.  Seleccione el grupo de actualizaciones de software que quiere implementar.  

4.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**. Se abre el **Asistente para implementar actualizaciones de software** .  

5.  En la página General, configure las siguientes opciones:  

    -   **Nombre**: especifique el nombre para la implementación. La implementación debe tener un nombre único que describa su propósito, y la diferencie de otras implementaciones del sitio de Configuration Manager. De forma predeterminada, Configuration Manager asigna automáticamente un nombre para la implementación con el siguiente formato: **Actualizaciones de Microsoft Software -** <*fecha*><*hora*>.  

    -   **Descripción:**especifique una descripción para la implementación. La descripción proporciona información general de la implementación, además de cualquier otra información pertinente que permita identificar y diferenciar esta del resto de implementaciones del sitio de Configuration Manager. El campo de descripción es opcional, tiene un límite de 256 caracteres y tiene un valor en blanco de forma predeterminada.  

    -   **Actualización de software/Grupo de actualizaciones de software**: compruebe que la actualización de software, o el grupo de actualizaciones de software es el correcto.  

    -   **Seleccionar plantilla de implementación**: especifique si quiere aplicar una plantilla de implementación guardada anteriormente. Puede configurar una plantilla de implementación que contenga propiedades comunes de implementación de software para, luego, implementar la plantilla en actualizaciones de software posteriores para, así, garantizar la coherencia entre implementaciones similares y ahorrar tiempo.  

    -   **Recopilación**: especifique la recopilación para la implementación, según corresponda. los miembros de la recopilación reciben las actualizaciones de software definidas en la implementación.  

6.  En la página Configuración de implementación, configure las siguientes opciones:  

    -   **Tipo de implementación**: especifique el tipo de implementación para la implementación de actualizaciones de software. Seleccione **Requerido** para crear una implementación de actualización de software obligatoria en la que las actualizaciones de software se instalan automáticamente en los clientes antes de una fecha límite configurada. Seleccione **Disponible** para crear una implementación de actualización de software que esté disponible para que los usuarios la instalen desde el Centro de software.  

        > [!IMPORTANT]  
        >  Una vez creada la implementación de actualización de software, no podrá cambiar el tipo de implementación.  

        > [!NOTE]  
        >  Un grupo de actualizaciones de software implementado como **Requerido** se descargará en segundo plano y se respetará la configuración de BITS, si ha configurado.  
        > Sin embargo, los grupos de actualizaciones de software implementados como **Disponible** se descargarán en primer plano y omitirán la configuración de BITS.  

    -   **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas**: especifique si quiere habilitar Wake on LAN en la fecha límite para enviar paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. Los equipos que estén en modo de suspensión en la fecha límite de instalación se activarán para que se pueda iniciar la instalación de las actualizaciones de software. Los clientes que están en modo de suspensión pero no requieren actualizaciones de software de la implementación no se iniciarán. De forma predeterminada, esta opción no está habilitada. Sólo está disponible cuando **Tipo de implementación** está establecido en **Requerido**.  

        > [!WARNING]  
        >  Para poder utilizar esta opción, los equipos y las redes deben configurarse para Wake on LAN.  

    -   **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado que notifican los equipos cliente.  

7.  En la página Programación, configure las siguientes opciones:  

    -   **Programar evaluación**: especifique si la hora disponible y las horas de fecha límite de instalación se evalúan mediante la hora UTC o la hora local del equipo que ejecuta la consola de Configuration Manager.  

        > [!NOTE]  
        >  Al seleccionar la hora local y luego **Lo antes posible** para **Horas de disponibilidad del software** o **Fecha límite de instalación**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles o cuándo se instalan en un cliente. Si el cliente está en una zona horaria distinta, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.  

    -   **Horas de disponibilidad del software**: seleccione una de las siguientes opciones a fin de especificar cuándo estarán disponibles las actualizaciones de software para los clientes:  

        -   **Lo antes posible**: seleccione esta opción a fin de que las actualizaciones de software de la implementación estén disponibles para los equipos clientes lo antes posible. Al crearse la implementación, se actualiza la directiva de cliente, los clientes conocen la existencia de la implementación con el siguiente ciclo de sondeo de directiva de cliente, lo cual permite que las actualizaciones estén disponibles para la instalación.  

        -   **Hora específica**: seleccione esta opción a fin de que las actualizaciones de software incluidas en la implementación estén disponibles para los clientes en una fecha y hora concretas. Al crearse la implementación, se actualiza la directiva de cliente, y los clientes conocen la existencia de la implementación con el siguiente ciclo de sondeo de directiva de cliente. Sin embargo, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora especificada.  

    -   **Fecha límite de instalación**: seleccione una de las siguientes opciones para especificar la fecha de límite de instalación de las actualizaciones de software de la implementación.  

        > [!NOTE]  
        >  Sólo puede configurar la opción de fecha límite de instalación si **Tipo de implementación** está establecido en **Requerido** en la página Configuración de implementación.  

        -   **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.  

        -   **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente en una fecha y hora concretas.  

        > [!NOTE]  
        >  La hora real de la fecha límite de instalación es la hora que se configure más una cantidad aleatoria de tiempo de hasta 2 horas. Se minimiza, así, el efecto negativo que podría producirse si todos los equipos cliente de la recopilación de destino instalan las actualizaciones de software de la implementación a la misma hora.  
        >   
        >  Puede establecer la opción **Deshabilitar selección aleatoria de fecha límite** de la configuración de cliente **Agente de equipo** para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones de software requeridas. Para obtener más información, vea [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  En la página Experiencia del usuario, configure las siguientes opciones:  

    -   **Notificaciones de usuario**: especifique si quiere mostrar una notificación de las actualizaciones de software en el Centro de software del equipo cliente según las **Horas de disponibilidad del software** y si quiere mostrar las notificaciones de usuario en los equipos cliente. Si **Tipo de implementación** está establecido en **Disponible** en la página Configuración de implementación, no se puede seleccionar **Ocultar en el Centro de software y ocultar todas las notificaciones**.  

    -   **Comportamiento de la fecha límite**: solo disponible cuando **Tipo de implementación** está establecido en **Requerido** en la página Configuración de implementación.   
    especifique el comportamiento que tiene lugar cuando se alcanza la fecha límite para la implementación de actualizaciones de software. Especifique si desea instalar las actualizaciones de software de la implementación. Especifique también si el sistema se debe reiniciar tras la instalación de las actualizaciones de software independientemente de lo establecido en una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamiento de reinicio de dispositivo**: solo disponible cuando **Tipo de implementación** está establecido en **Requerido** en la página Configuración de implementación.    
    especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de actualizaciones de software en servidores y estaciones de trabajo.  

        > [!IMPORTANT]  
        >  Suprimir los reinicios de sistema puede ser útil en entornos de servidor o si no desea que los equipos que instalan las actualizaciones de software se reinicien de manera predeterminada. Sin embargo, esta opción puede dejar a los equipos en un estado poco seguro; por su lado, forzar el reinicio permite asegurar que la instalación de actualizaciones de software se completa inmediatamente.

    -   **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: cuando implemente actualizaciones de software en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que las actualizaciones de software se instalen en la superposición temporal y, o bien confirmar los cambios más tarde, o bien confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

        > [!NOTE]  
        >  Cuando implemente una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada.  

    - **Comportamiento de reevaluación de implementación de actualizaciones de software tras el reinicio**: a partir de la versión 1606 de Configuration Manager, seleccione esta opción para configurar implementaciones de actualizaciones de software para que los clientes ejecuten un examen de cumplimiento de actualizaciones de software inmediatamente después de que un cliente instale las actualizaciones de software y se reinicie. Esto permite al cliente comprobar las actualizaciones de software adicionales que entran en vigor después de que el cliente reinicie e instalarlas (para cumplir así los requisitos) durante la misma ventana de mantenimiento.

9. En la página Alertas, configure cómo generarán Configuration Manager y System Center Operations Manager las alertas para esta implementación. Sólo se pueden configurar alertas si **Tipo de implementación** está establecido en **Requerido** en la página Configuración de implementación.  

    > [!NOTE]  
    >  Puede revisar las alertas de las actualizaciones de software recientes en el área de trabajo **Biblioteca de software** del nodo **Actualizaciones de software** .  

10. En la página Configuración de descarga, configure las siguientes opciones:  

    - Especifique si el cliente descargará e instalará las actualizaciones de software cuando esté conectado a una red lenta o si utiliza una ubicación de contenido de reserva.  

    - Especifique si el cliente debe descargar e instalar las actualizaciones de software desde un punto de distribución de reserva cuando el contenido de las actualizaciones de software no está disponible en un punto de distribución preferido.  

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si quiere habilitar el uso de BranchCache para las descargas de contenido. Para obtener más información sobre BranchCache, consulte [Conceptos básicos de la administración de contenido](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **If software updates are not available on distribution point in current, neighbor or site groups, download content from Microsoft Updates** (Si las actualizaciones de software no están disponibles en el punto de distribución actual en el grupo actual, vecino o de sitio, descargue el contenido de Microsoft Updates): seleccione esta opción para que los clientes que están conectados a la intranet descarguen las actualizaciones de software desde Microsoft Update si las actualizaciones de software no están disponibles en los puntos de distribución. Los clientes basados en Internet siempre pueden ir a Microsoft Update para obtener el contenido de las actualizaciones de software.

    - Especifique si desea permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

    > [!NOTE]  
    >  Los clientes solicitan la ubicación del contenido desde un punto de administración para las actualizaciones de software de una implementación. El comportamiento de descarga depende de cómo se hayan configurado el punto de distribución, el paquete de implementación y las opciones de esta página. Para obtener más información, vea [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md) (Escenarios de ubicación de origen del contenido).  

11. Si ha realizado el [Paso 3: descargar el contenido para el grupo de actualizaciones de software](#BKMK_3DownloadContent), las páginas Paquete de implementación, Puntos de distribución y Selección del idioma no se mostrarán, y puede ir al paso 15 del asistente.  

    > [!IMPORTANT]  
    >  Las actualizaciones de software que ya se descargaron en la biblioteca de contenido del servidor del sitio no se descargan de nuevo, aunque se cree un paquete de implementación nuevo para las actualizaciones de software. Si ya se descargaron todas las actualizaciones de software, el asistente pasa a la página **Selección del idioma** (paso 15).  

12. En la página Paquete de implementación, seleccione un paquete de implementación existente o configure las siguientes opciones para especificar un paquete de implementación nuevo:  

    1.  **Nombre**: especifique el nombre del paquete de implementación. Debe ser un nombre único que describe el contenido del paquete. Está limitado a 50 caracteres.  

    2.  **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción está limitada a 127 caracteres.  

    3.  **Origen de paquete**: especifique la ubicación de los archivos de origen de la actualización de software.  Escriba una ruta de red de la ubicación de los archivos de origen, por ejemplo, **\\\servidor\nombre de recurso compartido\ruta**, o haga clic en **Examinar** para buscar la ubicación de red. Debe crear la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la siguiente página.  

        > [!NOTE]  
        >  Ningún otro paquete de implementación de software podrá usar la ubicación de origen del paquete de implementación que especifique.  

        > [!IMPORTANT]  
        >  Tanto la cuenta de equipo del proveedor de SMS como el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos NTFS de **escritura** en la ubicación de descarga. Debe restringir cuidadosamente el acceso a la ubicación de descarga para reducir el riesgo de alteración de los archivos de origen de la actualización de software por parte de atacantes.  

        > [!IMPORTANT]  
        >  Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Pero si lo hace, primero debe copiar el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  

    4.  **Prioridad de envío**: especifique la prioridad de envío del paquete de implementación. Configuration Manager usa la prioridad de envío para el paquete de implementación cuando envía el paquete a los puntos de distribución. Los paquetes de implementación se envían en orden de prioridad: Alta, Media, o Baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesará inmediatamente sin tener en cuenta su prioridad.  

13. En la página Puntos de distribución, especifique los puntos de distribución o los grupos de puntos de distribución que hospedarán los archivos de actualización de software. Para más información sobre los puntos de distribución, vea [Distribution point configurations (Configuraciones de puntos de distribución)](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. En la página Ubicación de descarga, especifique si los archivos de actualización de software se van a descargar desde Internet o desde la red local. Configure las siguientes opciones:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde una ubicación de Internet especificada. Esta opción está habilitada de forma predeterminada.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones de software desde una carpeta local o una carpeta de red compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Las actualizaciones de software se descargan de forma preliminar desde cualquier equipo que tenga acceso a Internet, y se almacenan en una ubicación de la red local donde se podrá acceder para la instalación.  

15. En la página Selección del idioma, seleccione los idiomas para los que se descargan las actualizaciones de software seleccionadas. Las actualizaciones de software sólo se descargan si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no utilicen ningún idioma específico se descargarán siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si sólo selecciona idiomas no admitidos por una actualización de software, la descarga no se completará para tal actualización.  

16. En la página Resumen, revise la configuración. Para guardar la configuración en una plantilla de implementación, haga clic en **Guardar como plantilla**, escriba un nombre, seleccione la configuración que va a incluir en la plantilla y, a continuación, haga clic en **Guardar**. Para cambiar una configuración, haga clic en la página correspondiente del asistente y cámbiela.  

    > [!WARNING]  
    >  El nombre de plantilla puede incluir caracteres ASCII alfanumérico, **\\** (barra diagonal inversa) y **‘** (comillas tipográficas).  

17. Haga clic en **Siguiente** para implementar la actualización de software.  

 Una vez completado el asistente, Configuration Manager descarga las actualizaciones de software en la biblioteca de contenido del servidor del sitio, distribuye las actualizaciones a los puntos de distribución configurados y, a continuación, implementa el grupo de actualizaciones de software en los clientes de la recopilación de destino. Para obtener más información sobre el proceso de implementación, consulte [Proceso de implementación de actualizaciones de software](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Pasos siguientes
[Supervisar actualizaciones de software](monitor-software-updates.md)
