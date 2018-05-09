---
title: Implementar actualizaciones de software automáticamente
titleSuffix: Configuration Manager
description: Implemente actualizaciones de software automáticamente al agregar nuevas actualizaciones de software a un grupo de actualizaciones asociado a una implementación activa, o bien mediante el empleo de reglas de ADR.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3b267e122370cc12ecec2f42dcb1dfc62c45fe63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_AutoDeploy"></a> Implementar actualizaciones de software automáticamente  

*Se aplica a: System Center Configuration Manager (Rama actual)*

 Se puede usar una regla de implementación automática (ADR) en lugar de agregar actualizaciones nuevas a un grupo de actualización de software existente. Normalmente, las ADR se usan para implementar actualizaciones de software mensuales (conocidas como actualizaciones "Patch Tuesday") y para administrar las actualizaciones de definiciones. Si necesita ayuda para determinar qué método de implementación es el adecuado para usted, vea [Deploy software updates](deploy-software-updates.md) (Implementación de actualizaciones de software).

<!--##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  --mstewart this is already doc'd on the SUG page. -->

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Crear una regla de implementación automática (ADR)  
Las actualizaciones de software se pueden aprobar e implementar automáticamente mediante una ADR. Puede hacer que la regla agregue las actualizaciones de software a un nuevo grupo de actualización de software cada vez que dicha regla se ejecute o que agregue las actualizaciones de software a un grupo existente. Cuando una regla se ejecuta y agrega actualizaciones de software a un grupo existente, quita todas las actualizaciones del grupo y luego agrega las que cumplan los criterios que se hayan definido para el grupo. 

> [!WARNING]  
>  Antes de crear una ADR por primera vez, compruebe que se completó la sincronización de las actualizaciones de software en el sitio. Esto es importante si se ejecuta Configuration Manager en un idioma que no sea el inglés, porque las clasificaciones de actualizaciones de software se muestran en inglés antes de la primera sincronización y, después, en el idioma localizado una vez completada la sincronización de las actualizaciones de software. Las reglas creadas antes de sincronizar las actualizaciones de software podrían no funcionar correctamente tras la sincronización porque la cadena de texto podría no coincidir.  

 Use el procedimiento siguiente para crear una ADR.  

#### <a name="to-create-an-adr"></a>Para crear una ADR  

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software****Información general** > **Actualizaciones de software** > **Reglas de implementación automática**.  

2.  En la pestaña **Inicio** , en el grupo **Crear** , haga clic en **Crear regla de implementación automática**. Se abre el Asistente para crear regla de implementación automática.  

3.  En la página **General** , configure las siguientes opciones:  

    -   **Nombre**: especifique el nombre de la ADR. El nombre debe ser único, describir el objetivo de la regla e identificarla entre el resto de reglas del sitio de Configuration Manager.  

    -   **Descripción**: especifique una descripción para la ADR. La descripción debería proporcionar información general de la regla implementación y otra información relevante que ayude a diferenciar esta regla de otras. El campo de descripción es opcional, tiene un límite de 256 caracteres y tiene un valor en blanco de forma predeterminada.  

    -   **Seleccionar plantilla de implementación**: especifique si quiere aplicar una plantilla de implementación guardada anteriormente. Se puede configurar una plantilla de implementación que contenga varias propiedades de implementación de actualización comunes que se puedan usar para crear las ADR. Estas plantillas permiten garantizar la coherencia en implementaciones similares y ahorrar tiempo.  

         - Puede elegir entre las plantillas de implementación de actualización de software integradas del Asistente para crear regla de implementación automática. La plantilla **Actualizaciones de definiciones** proporciona opciones de configuración comunes para implementar actualizaciones de definiciones de software. La plantilla **Patch Tuesday** proporciona opciones de configuración comunes para implementar actualizaciones de software en un ciclo mensual.  

    -   **Recopilación**: especifica la recopilación de destino que se utilizará para la implementación. los miembros de la recopilación reciben las actualizaciones de software definidas en la implementación.  

    -   Decida si desea agregar las actualizaciones de software a un grupo de actualizaciones de software nuevo o a uno existente. En la mayoría de los casos, probablemente, elegirá crear un nuevo grupo de actualizaciones de software cuando se ejecuta la regla de implementación automática. Sin embargo, podría optar por un grupo existente si la regla se ejecuta con una programación más exigente. Por ejemplo, si va a ejecutar la regla diariamente para las actualizaciones de definiciones, podría agregar las actualizaciones de software a un grupo de actualizaciones de software existente.  

    -   **Habilitar la implementación después de ejecutar la regla**: especifique si quiere habilitar la implementación de actualizaciones de software después de la ejecución de la regla de implementación automática. En cuanto a esta especificación, considere los aspectos siguientes:  

        -   Cuando se habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. El contenido de actualización de software se descarga según sea necesario. El contenido se copia en los puntos de distribución especificados y las actualizaciones se implementan en los clientes de la recopilación de destino.  

        -   Cuando no se habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. Se configura la directiva de implementación de actualizaciones de software. Pero las actualizaciones no se descargan ni implementan en los clientes. Esta situación proporciona tiempo para preparar la implementación de las actualizaciones, comprobar que las actualizaciones que cumplen los criterios son adecuadas y habilitar la implementación posteriormente.  

4.  En la página Configuración de implementación, configure las siguientes opciones:  

    -   **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas**: especifica si se debe habilitar Wake on LAN en la fecha límite para enviar paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. Los equipos que estén en modo de suspensión en la fecha límite de instalación se activarán para que se pueda iniciar la instalación. Los clientes que están en modo de suspensión pero no requieren actualizaciones de software de la implementación no se iniciarán. De forma predeterminada, esta opción no está habilitada. Para poder utilizar esta opción, debe configurar los equipos y redes para Wake On LAN. 

    -   **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado que notifican los equipos cliente.  

        > [!IMPORTANT]  
        >  Cuando implemente actualizaciones de definiciones, establezca el nivel de detalle en **Solo error** para que el cliente notifique un mensaje de estado solo cuando se produzca un error en la actualización de definiciones. De lo contrario, el número de mensajes de estado que notifique el cliente podría afectar al rendimiento en el servidor del sitio.  

    -   **Configuración de términos de licencia**: especifique si quiere implementar automáticamente las actualizaciones de software con los términos de licencia asociados. Algunas actualizaciones de software incluyen términos de licencia, como, por ejemplo, un Service Pack. Cuando se implementan automáticamente actualizaciones de software, no se muestran los términos de licencia, y no se da la opción de aceptarlos. Puede elegir implementar automáticamente todas las actualizaciones de software independientemente de si tienen términos de licencia asociados, o bien implementar solo las actualizaciones que no tengan términos de licencia asociados.  
        - Para revisar los términos de licencia de una actualización de software, selecciónela en el nodo **Todas las actualizaciones de software** del área de trabajo **Biblioteca de software**. En la pestaña **Inicio**, en el grupo **Actualizar**, haga clic en **Revisar la licencia**.    
        - Para buscar actualizaciones de software con términos de licencia asociados, se puede agregar la columna **Términos de licencia** al panel de resultados del nodo **Todas las actualizaciones de software**. Haga clic en el encabezado de la columna para ordenar por actualizaciones de software con términos de licencia.  

5.  En la página Actualizaciones de software, configure los criterios para las actualizaciones de software que la regla de implementación automática recupera y agrega al grupo de actualizaciones de software. El límite para las actualizaciones de software en la regla de implementación automática es de 1000 actualizaciones de software. Si es necesario, se puede filtrar por el tamaño del contenido de las actualizaciones de software en las reglas de implementación automática. Para más información, vea [Configuration Manager and Simplified Windows Servicing on Down Level Operating Systems (Configuration Manager y mantenimiento simplificado de Windows en sistemas operativos de nivel inferior)](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).


6.  En la página Programación de evaluación, especifique si quiere habilitar la regla de implementación automática para que se ejecute en función de una programación. Si la habilita, haga clic en **Personalizar** para configurar la programación periódica. La configuración de la hora de inicio para la programación se basa en la hora local del equipo que ejecuta la consola de Configuration Manager.
    - La configuración de la hora de inicio para la programación se basa en la hora local del equipo que ejecuta la consola de Configuration Manager.
    - La evaluación de regla de implementación automática puede ejecutar tres veces al día.
    - No establezca nunca la programación de evaluación con una frecuencia que supere la programación de sincronización de actualizaciones de software. La programación de sincronización de punto de actualización de software se muestra para que se pueda determinar la frecuencia de la programación de evaluación. 
    - Para ejecutar manualmente la regla de implementación automática, seleccione la regla y luego haga clic en **Ejecutar ahora** en la pestaña **Inicio** del grupo **Regla de implementación automática** .
    
       > [!NOTE]  
       >A partir de la versión 1802 de Configuration Manager, se pueden programar ADR para evaluar el desplazamiento con respecto a un día base. Es decir, si la revisión del martes en su caso cae en miércoles, se puede establecer la programación de evaluación para el segundo martes del mes con un desplazamiento de un día. <!--1357133-->
       > - Al programar la evaluación para que se produzca con un desplazamiento durante la última semana del mes, la evaluación se programará para el último día del mes si el desplazamiento elegido se desborda en el mes siguiente. <!--506731-->

       > ![Desplazamiento de la programación de evaluación personalizada de ADR desde el día base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  En la página Programación de implementación, configure las siguientes opciones:  

    -   **Programar evaluación**: especifique si Configuration Manager evalúa la hora disponible y las horas límite de instalación mediante la hora UTC o la hora local del equipo que ejecuta la consola de Configuration Manager.  
         - Al seleccionar la hora local y luego **Lo antes posible** para **Horas de disponibilidad del software** o **Fecha límite de instalación**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles o cuándo se instalan en un cliente. Si el cliente está en una zona horaria distinta, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.  

    -   **Horas de disponibilidad del software**: seleccione una de las siguientes opciones a fin de especificar cuándo estarán disponibles las actualizaciones de software para los clientes:  

        -   **Lo antes posible**: hace que las actualizaciones de software incluidas en la implementación estén disponibles para los equipos cliente lo antes posible. Si se crea la implementación con esta opción seleccionada, Configuration Manager actualiza la directiva del cliente. En el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación y pueden obtener las actualizaciones disponibles para la instalación.  

        -   **Hora específica**: hace que las actualizaciones de software incluidas en la implementación estén disponibles para los clientes en una fecha y hora concretas. Si se crea la implementación con esta opción habilitada, Configuration Manager actualiza la directiva del cliente. Con el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación. Sin embargo, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora configurada.  

    -   **Fecha límite de instalación**: seleccione una de las siguientes opciones para especificar la fecha de límite de instalación de las actualizaciones de software de la implementación:  

        -   **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.  

        -   **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente en una fecha y hora concretas. Configuration Manager determina la fecha límite para instalar actualizaciones de software, para lo cual agrega el intervalo **Hora específica** establecido a **Horas de disponibilidad del software**.  

            - La hora de la fecha límite de instalación real es la hora de la fecha límite más una cantidad aleatoria de tiempo de hasta dos horas. La selección aleatoria reduce el posible impacto de los equipos cliente de la recopilación que instalan las actualizaciones en la implementación a la misma hora.  
          
             - Puede establecer la opción **Deshabilitar selección aleatoria de fecha límite** de la configuración de cliente **Agente de equipo** para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones de software requeridas. Para más información, vea [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. En la página Experiencia del usuario, configure las siguientes opciones:  

    -   **Notificaciones de usuario**: especifique si quiere mostrar una notificación de las actualizaciones de software en el Centro de software del equipo cliente según las **Horas de disponibilidad del software** y si quiere mostrar las notificaciones de usuario en los equipos cliente.  

    -   **Comportamiento de la fecha límite**: especifique el comportamiento que tiene lugar cuando se alcanza la fecha límite para la implementación de actualizaciones de software. Especifique si desea instalar las actualizaciones de software de la implementación. Especifique también si el sistema se debe reiniciar tras la instalación de las actualizaciones de software independientemente de lo establecido en una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamiento de reinicio de dispositivo**: especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de actualizaciones en servidores y estaciones de trabajo.  

        > [!WARNING]  
        >  Suprimir los reinicios de sistema puede ser útil en entornos de servidor, si no desea que los equipos que instalan las actualizaciones de software se reinicien de manera predeterminada. Sin embargo, esta opción puede dejar a los equipos en un estado poco seguro; por su lado, forzar el reinicio permite asegurar que la instalación de actualizaciones de software se completa inmediatamente.  

    -   **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: cuando implemente actualizaciones de software en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que las actualizaciones de software se instalen en la superposición temporal y, o bien confirmar los cambios más tarde, o bien confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

           -  Cuando implemente una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo sea miembro de una recopilación que tenga una ventana de mantenimiento configurada.  

    - **Comportamiento de reevaluación de implementación de actualizaciones de software tras el reinicio**: seleccione esta opción para configurar las implementaciones de actualizaciones de software para que los clientes ejecuten un examen de cumplimiento de actualizaciones de software inmediatamente después de que un cliente instale las actualizaciones de software y se reinicie. Esta opción permite al cliente comprobar las actualizaciones adicionales que entran en vigor después de que el cliente se reinicie y luego las instala durante la misma ventana de mantenimiento.

9. En la página Alertas, configure cómo generarán Configuration Manager y System Center Operations Manager las alertas para esta implementación. Puede revisar las alertas de las actualizaciones de software recientes en el área de trabajo **Biblioteca de software** del nodo **Actualizaciones de software** .  

10. En la página Configuración de descarga, configure las siguientes opciones:  

    - Especifique si los clientes deben descargar e instalar las actualizaciones cuando estén conectados a una red lenta o si usan una ubicación de contenido de reserva.  

    - Especifique si los clientes tienen que descargar e instalar las actualizaciones de software desde un punto de distribución de reserva cuando el contenido de las actualizaciones de software no está disponible en un punto de distribución preferido.  

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si quiere habilitar el uso de BranchCache para las descargas de contenido. Para más información sobre BranchCache, vea [Concepts for content management (Conceptos para la administración de contenido)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Si las actualizaciones de software no están disponibles en un punto de distribución del grupo de límites actual, vecino o del sitio, descargue el contenido de Microsoft Update**: seleccione esta opción para que los clientes que están conectados a la intranet descarguen las actualizaciones de software desde Microsoft Update si las actualizaciones de software no están disponibles en los puntos de distribución. Los clientes basados en Internet siempre pueden ir a Microsoft Update para obtener el contenido de las actualizaciones de software.

    - Especifique si desea permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

    > [!NOTE]  
    >  Los clientes solicitan la ubicación del contenido desde un punto de administración para las actualizaciones de software de una implementación. El comportamiento de descarga depende de cómo se hayan configurado el punto de distribución, el paquete de implementación y las opciones de esta página. Para obtener más información, vea [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md) (Escenarios de ubicación de origen del contenido).  

11. En la página Paquete de implementación, seleccione un paquete de implementación existente o configure las opciones siguientes para crear un nuevo paquete de implementación:  

    1.  **Nombre**: especifique el nombre del paquete de implementación. Use un nombre único que describa el contenido del paquete. Está limitado a 50 caracteres.  

    2.  **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción está limitada a 127 caracteres.  

    3.  **Origen de paquete**: especifica la ubicación de los archivos de origen de la actualización de software.  Escriba una ruta de red de la ubicación de los archivos de origen, por ejemplo, **\\\servidor\nombre de recurso compartido\ruta**, o haga clic en **Examinar** para buscar la ubicación de red. Cree la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la página siguiente.  

        - Ningún otro paquete de implementación de software puede usar la ubicación de origen del paquete de implementación especificado.
        - Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Pero si lo hace, primero debe copiar el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  
        -  Tanto la cuenta de equipo del proveedor de SMS como el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos NTFS de **escritura** en la ubicación de descarga. Debe restringir cuidadosamente el acceso a la ubicación de descarga para reducir el riesgo de alteración de los archivos de origen de la actualización de software por parte de atacantes.  
       

    4.  **Prioridad de envío**: especifique la prioridad de envío del paquete de implementación. Configuration Manager usa la prioridad de envío para el paquete de implementación cuando envía el paquete a los puntos de distribución. Los paquetes de implementación se envían en orden de prioridad: Alta, Media, o Baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesará inmediatamente sin tener en cuenta su prioridad.  

12. En la página Puntos de distribución, especifique los puntos de distribución o los grupos de puntos de distribución que hospedarán los archivos de actualización de software. Para más información sobre los puntos de distribución, vea [Distribution point configurations (Configuraciones de puntos de distribución)](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Esta página sólo está disponible cuando se crea un nuevo paquete de implementación de actualizaciones de software.
  

13. En la página Ubicación de descarga, especifique si los archivos de actualización de software se van a descargar desde Internet o desde la red local. Configure las siguientes opciones:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde una ubicación de Internet especificada. Esta opción está habilitada de forma predeterminada.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones de software desde un directorio local o una carpeta compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Cualquier equipo con acceso a Internet puede descargar de forma preliminar las actualizaciones de software y almacenarlas en una ubicación de la red local a la que se pueda tener acceso desde el equipo que ejecuta el asistente.  

14. En la página Selección del idioma, seleccione los idiomas para los que se descargan las actualizaciones de software seleccionadas. Las actualizaciones de software sólo se descargan si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no utilicen ningún idioma específico se descargarán siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si solo selecciona idiomas no admitidos por una actualización de software, se producirá un error en la descarga de la actualización.  

15. En la página Resumen, revise la configuración. Para guardar la configuración en una plantilla de implementación, haga clic en **Guardar como plantilla**. Escriba un nombre, seleccione la configuración que quiere incluir en la plantilla y, después, haga clic en **Guardar**. Para cambiar una configuración, haga clic en la página correspondiente del asistente y cámbiela.  
    -  El nombre de plantilla puede incluir caracteres ASCII alfanumérico, **\\** (barra diagonal inversa) y **‘** (comillas tipográficas).  

16. Haga clic en **Siguiente** crear la regla de implementación automática (ADR).  

 Una vez completado el asistente, se ejecutará la ADR. Agregará las actualizaciones de software que cumplen los criterios especificados a un grupo de actualizaciones de software. Después, la ADR descarga las actualizaciones de la biblioteca de contenido en el servidor de sitio y las distribuye a los puntos de distribución configurados. Luego, la ADR implementa el grupo de actualizaciones de software en los clientes de la recopilación de destino.  

##  <a name="BKMK_AddDeploymentToADR"></a> Agregar una nueva implementación a una ADR existente  
 Después de crear una ADR, puede agregar implementaciones adicionales a la regla. Esto puede ayudarle a administrar la complejidad de la implementación de varias actualizaciones en diferentes recopilaciones. Cada nueva implementación ofrece todas las funcionalidades y la experiencia completa de supervisión de la implementación.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Para agregar una nueva implementación a una ADR existente  

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Información general** > **Actualizaciones de software** > **Reglas de implementación automática** y luego seleccione la regla que quiera.  

2.  En la pestaña **Inicio** , del grupo **Regla de implementación automática** , haga clic en **Agregar implementación**. Se abrirá el Asistente para agregar implementaciones.  

3.  En la página **Recopilación** , configure las siguientes opciones:  

    -   **Recopilación**: especifica la recopilación de destino que se utilizará para la implementación. los miembros de la recopilación reciben las actualizaciones de software definidas en la implementación.  

    -   **Habilitar la implementación después de ejecutar la regla**: especifique si quiere habilitar la implementación de actualizaciones de software después de la ejecución de la regla de implementación automática. En cuanto a esta especificación, considere los aspectos siguientes:  

        -   Cuando se habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. El contenido de actualización de software se descarga según sea necesario. El contenido se copia en los puntos de distribución especificados y las actualizaciones se implementan en los clientes de la recopilación de destino.  

        -  Cuando no se habilita la implementación, las actualizaciones que cumplen los criterios definidos de la regla se agregan a un grupo de actualizaciones de software. Se configura la directiva de implementación de actualizaciones de software. Pero las actualizaciones no se descargan ni implementan en los clientes. Esta situación proporciona tiempo para preparar la implementación de las actualizaciones, comprobar que las actualizaciones que cumplen los criterios son adecuadas y habilitar la implementación posteriormente.  

4.  En la página Configuración de implementación, configure las siguientes opciones:  

    -   **Usar Wake-on-LAN para activar clientes para las implementaciones requeridas**: especifica si se debe habilitar Wake on LAN en la fecha límite para enviar paquetes de reactivación a equipos que requieran una o varias actualizaciones de software en la implementación. Los equipos que estén en modo de suspensión en la fecha límite de instalación se activarán para que se pueda iniciar la instalación. Los clientes que están en modo de suspensión pero no requieren actualizaciones de software de la implementación no se iniciarán. De forma predeterminada, esta opción no está habilitada. Para poder utilizar esta opción, debe configurar los equipos y redes para Wake On LAN.  

    -   **Nivel de detalle**: especifique el nivel de detalle de los mensajes de estado que notifican los equipos cliente.  

        > [!IMPORTANT]  
        >  Cuando implemente actualizaciones de definiciones, configure el nivel de detalle en **Sólo error** para que el cliente notifique un mensaje de estado sólo cuando no se pueda entregar una definición de estado al cliente. De lo contrario, el número de mensajes de estado que notifique el cliente podría afectar al rendimiento en el servidor del sitio.  

5.  En la página Programación de implementación, configure las siguientes opciones:  

    -   **Programar evaluación**: especifique si Configuration Manager evalúa la hora disponible y las horas límite de instalación mediante la hora UTC o la hora local del equipo que ejecuta la consola de Configuration Manager.  

           -  Al seleccionar la hora local y luego **Lo antes posible** para **Horas de disponibilidad del software** o **Fecha límite de instalación**, la hora actual en el equipo que ejecuta la consola de Configuration Manager se usa para evaluar cuándo hay actualizaciones disponibles o cuándo se instalan en un cliente. Si el cliente está en una zona horaria distinta, estas acciones se producirán cuando la hora del cliente llegue a la hora de evaluación.  

    -   **Horas de disponibilidad del software**: seleccione una de las siguientes opciones a fin de especificar cuándo estarán disponibles las actualizaciones de software para los clientes:  

        -   **Lo antes posible**: seleccione esta opción a fin de que las actualizaciones de software incluidas en la implementación estén disponibles para los equipos cliente lo antes posible. Si se crea la implementación con esta opción seleccionada, Configuration Manager actualiza la directiva del cliente. En el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación y pueden obtener las actualizaciones disponibles para la instalación.  

        -   **Hora específica**: hace que las actualizaciones de software incluidas en la implementación estén disponibles para los clientes en una fecha y hora concretas. Si se crea la implementación con esta opción habilitada, Configuration Manager actualiza la directiva del cliente. Con el siguiente ciclo de sondeo de directiva de cliente, los clientes conocen la existencia de la implementación. Sin embargo, las actualizaciones de software de la implementación no están disponibles para la instalación hasta después de la fecha y hora configurada. 

    -   **Fecha límite de instalación**: seleccione una de las siguientes opciones para especificar la fecha de límite de instalación de las actualizaciones de software de la implementación:  

        -   **Lo antes posible**: seleccione esta opción para que se instalen automáticamente las actualizaciones de software incluidas en la implementación lo antes posible.  

        -   **Hora específica**: seleccione esta opción para que las actualizaciones de software de la implementación se instalen automáticamente en una fecha y hora concretas. Configuration Manager determina la fecha límite para instalar actualizaciones de software, para lo cual agrega el intervalo **Hora específica** establecido a **Horas de disponibilidad del software**.  

               - La hora de la fecha límite de instalación real es la hora de la fecha límite más una cantidad aleatoria de tiempo de hasta dos horas. Esto reduce el posible impacto de los equipos cliente de la recopilación que instalan las actualizaciones en la implementación a la misma hora.  
              - Puede establecer la opción **Deshabilitar selección aleatoria de fecha límite** de la configuración de cliente **Agente de equipo** para deshabilitar el retraso de la selección aleatoria de instalación para las actualizaciones de software requeridas. Para más información, vea [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  En la página Experiencia del usuario, configure las siguientes opciones:  

    -   **Notificaciones de usuario**: especifique si quiere mostrar una notificación de las actualizaciones de software en el Centro de software del equipo cliente según las **Horas de disponibilidad del software** y si quiere mostrar las notificaciones de usuario en los equipos cliente.  

    -   **Comportamiento de la fecha límite**: especifique el comportamiento que tiene lugar cuando se alcanza la fecha límite para la implementación de actualizaciones de software. Especifique si desea instalar las actualizaciones de software de la implementación. Especifique también si el sistema se debe reiniciar tras la instalación de las actualizaciones de software independientemente de lo establecido en una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamiento de reinicio de dispositivo**: especifique si se debe suprimir el reinicio del sistema necesario para completar la instalación de actualizaciones en servidores y estaciones de trabajo.  
 
           > [!WARNING]  
           >  Suprimir los reinicios de sistema puede ser útil en entornos de servidor, si no desea que los equipos que instalan las actualizaciones de software se reinicien de manera predeterminada. Sin embargo, esta opción puede dejar a los equipos en un estado poco seguro; por su lado, forzar el reinicio permite asegurar que la instalación de actualizaciones de software se completa inmediatamente.  

    - **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: cuando implemente actualizaciones de software en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que las actualizaciones de software se instalen en la superposición temporal y, o bien confirmar los cambios más tarde, o bien confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  

        - Cuando implemente una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada.  

7.  En la página Alertas, configure cómo generarán Configuration Manager y System Center Operations Manager las alertas para esta implementación. Puede revisar las alertas de las actualizaciones de software recientes en el área de trabajo **Biblioteca de software** del nodo **Actualizaciones de software** .  

8. En la página Configuración de descarga, configure las siguientes opciones:  

    - Especifique si los clientes deben descargar e instalar las actualizaciones de software cuando estén conectados a una red lenta o si usan una ubicación de contenido de reserva.  

    - Especifique si el cliente debe descargar e instalar las actualizaciones de software desde un punto de distribución de reserva cuando el contenido de las actualizaciones de software no está disponible en un punto de distribución preferido.  

    - **Permitir a los clientes compartir el contenido con otros clientes en la misma subred**: especifique si quiere habilitar el uso de BranchCache para las descargas de contenido. Para más información sobre BranchCache, vea [Concepts for content management (Conceptos para la administración de contenido)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Si las actualizaciones de software no están disponibles en un punto de distribución del grupo de límites actual, vecino o del sitio, descargue el contenido de Microsoft Update**: seleccione esta opción para que los clientes que están conectados a la intranet descarguen las actualizaciones de software desde Microsoft Update si las actualizaciones de software no están disponibles en los puntos de distribución. Los clientes basados en Internet siempre pueden ir a Microsoft Update para obtener el contenido de las actualizaciones de software.

    - Especifique si desea permitir que los clientes descarguen después de la fecha límite de instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que envía y recibe cuando se utiliza una conexión a Internet de uso medido.  

    > [!NOTE]  
    > Los clientes solicitan la ubicación del contenido desde un punto de administración para las actualizaciones de software de una implementación. El comportamiento de descarga depende de cómo se hayan configurado el punto de distribución, el paquete de implementación y las opciones de esta página. Para más información, vea [Escenarios de ubicación de orígenes de contenido](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Para más información sobre el proceso de implementación, vea [Software update deployment process (Proceso de implementación de actualizaciones de software)](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Pasos siguientes
[Supervisar actualizaciones de software](monitor-software-updates.md)
