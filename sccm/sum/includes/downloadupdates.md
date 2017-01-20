1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Actualizaciones de software**.  

2.  Elija la actualización de software que desee descargar mediante uno de los métodos siguientes:  

    -   Seleccione uno o varios grupos de actualizaciones de software en **Grupos de actualizaciones de software**y, a continuación, en la pestaña **Inicio** , en el grupo **Grupo de actualizaciones** , haga clic en **Descargar**.  

    -   Seleccione una o varias actualizaciones de software en **Todas las actualizaciones de software**y, a continuación, en la pestaña **Inicio** , en el grupo **Actualización** , haga clic en **Descargar**.  

        > [!NOTE]  
        >  En el nodo **Todas las actualizaciones de software**, Configuration Manager solo muestra actualizaciones de software con una clasificación de **Crítico** y **Seguridad** publicadas en los últimos 30 días.  

        > [!TIP]  
        >  Haga clic en **Agregar criterios** para filtrar las actualizaciones de software que se muestran en el nodo **Todas las actualizaciones de software** , guarde los criterios de búsqueda que use a menudo y, a continuación, administre las búsquedas guardadas en la pestaña **Búsqueda** .  

         Se abre el **Asistente para descargar actualizaciones de software** .  

3.  En la página **Paquete de implementación** , configure las siguientes opciones:  

    1.  **Seleccionar paquete de implementación**: elija esta opción a fin de seleccionar un paquete de implementación existente para las actualizaciones de software que se encuentran en la implementación.  

        > [!NOTE]  
        >  Las actualizaciones de software que ya se han descargado en el paquete de implementación seleccionado no se descargarán de nuevo.  

    2.  **Crear un nuevo paquete de implementación**: seleccione esta opción a fin de crear un nuevo paquete de implementación para las actualizaciones de software que se encuentran en la implementación. Configure las siguientes opciones:  

        -   **Nombre**: especifica el nombre del paquete de implementación. El paquete debe tener un nombre único que describa brevemente su contenido.  Está limitado a 50 caracteres.  

        -   **Descripción**: especifica la descripción del paquete de implementación. La descripción del paquete proporciona información sobre el contenido del paquete y se limita a 127 caracteres.  

        -   **Origen de paquete**: especifica la ubicación de los archivos de origen de la actualización de software. Escriba una ruta de red para la ubicación de origen, por ejemplo, **\\\servidor\nombreDeRecursoCompartido\ruta**, o haga clic en **Examinar** para buscar la ubicación de red. Debe crear la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar con la siguiente página.  

            > [!NOTE]  
            >  Ningún otro paquete de implementación de software podrá usar la ubicación de origen del paquete de implementación que especifique.  

            > [!IMPORTANT]  
            >  Tanto la cuenta de equipo del proveedor de SMS como el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos NTFS de **escritura** en la ubicación de descarga. Debe restringir cuidadosamente el acceso a la ubicación de descarga para reducir el riesgo de alteración de los archivos de origen de la actualización de software por parte de atacantes.  

            > [!IMPORTANT]  
            >  Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Pero si lo hace, primero debe copiar el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  

     Haga clic en **Siguiente**.  

4.  En la página **Puntos de distribución**, especifique los puntos de distribución o los grupos de puntos de distribución que hospedarán los archivos de actualización de software y, después, haga clic en **Siguiente**. Para obtener más información sobre los puntos de distribución, consulte [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) (Configuraciones de punto de distribución).  

    > [!NOTE]  
    >  La página Puntos de distribución solo está disponible cuando se crea un nuevo paquete de implementación de actualización de software.  

6.  En la página **Configuración de distribución**, especifique las opciones siguientes:  

    -   **Prioridad de distribución**: utilice esta opción para especificar la prioridad de distribución del paquete de implementación. La prioridad de distribución se aplica cuando se envía el paquete de implementación a puntos de distribución en sitios secundarios. Los paquetes de implementación se envían en orden de prioridad: **Alta**, **Media**, o **Baja**. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesará inmediatamente sin tener en cuenta su prioridad. De forma predeterminada, los paquetes se envían con prioridad **Mediana** .  

    -   **Distribuir el contenido de este paquete en puntos de distribución preferidos**: use esta opción para habilitar la distribución de contenido a petición en puntos de distribución preferidos. Cuando se habilita esta opción, el punto de administración crea un desencadenador para que el administrador de distribución distribuya el contenido en todos los puntos de distribución preferidos cuando un cliente solicite el contenido del paquete y el contenido no esté disponible en ningún punto de distribución preferido. Para obtener más información sobre los puntos de distribución preferidos y el contenido a petición, consulte [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md) (Escenarios de ubicación de origen de contenido).  

    -   **Configuración de punto de distribución preconfigurado**: utilice esta opción para especificar cómo quiere distribuir el contenido en los puntos de distribución preconfigurados. Elija una de las siguientes opciones:  

        -   **Descargar contenido automáticamente cuando los paquetes se asignen a puntos de distribución**: utilice esta opción para omitir los valores preconfigurados y distribuir contenido en el punto de distribución.  

        -   **Descargar solo los cambios de contenido en el punto de distribución**: utilice esta opción para preconfigurar el contenido inicial en el punto de distribución y luego distribuir los cambios de contenido en el punto de distribución.  

        -   **Copiar manualmente el contenido de este paquete en el punto de distribución**: utilice esta opción para preconfigurar siempre el contenido en el punto de distribución. Esta es la configuración predeterminada.  

         Para obtener más información sobre cómo preconfigurar contenido en puntos de distribución, consulte [Use Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)(Usar contenido preconfigurado).  

     Haga clic en **Siguiente**.  

6.  En la página **Ubicación de descarga**, especifique la ubicación que usará Configuration Manager para descargar los archivos de origen de la actualización de software. Utilice las siguientes opciones según sea necesario:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde la ubicación en Internet. Esta es la configuración predeterminada.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar actualizaciones de software desde una carpeta local o una carpeta de red compartida. Utilice esta opción cuando el equipo que ejecuta al asistente no tenga acceso a Internet.  

        > [!NOTE]  
        >  Cuando utilice esta opción, descargue las actualizaciones de software desde cualquier equipo con acceso a Internet y, a continuación, cópielas en una ubicación en la red local que sea accesible desde el equipo que ejecuta el asistente.  

     Haga clic en **Siguiente**.  

7.  En la página **Selección del idioma**, especifique los idiomas para los que se van a descargar las actualizaciones de software seleccionadas y haga clic en **Siguiente**. Configuration Manager descarga las actualizaciones de software solo si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no utilicen ningún idioma específico se descargarán siempre.  

8. En la página **Resumen**, compruebe la configuración seleccionada en el asistente y, después, haga clic en **Siguiente** para descargar las actualizaciones de software.  

9. En la página **Finalización**, compruebe que las actualizaciones de software se descargaron correctamente y, después, haga clic en **Cerrar**.  


<!--HONumber=Nov16_HO1-->


