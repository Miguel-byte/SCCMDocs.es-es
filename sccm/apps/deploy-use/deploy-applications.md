---
title: Implementar aplicaciones | System Center Configuration Manager
description: "Cree un tipo de implementación o simule la implementación de una aplicación con System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e608bcbadc82487018bb29c5e05660275d8fa275


---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*



 Antes de implementar una aplicación de System Center Configuration Manager, debe crear al menos un tipo de implementación para la aplicación. Para obtener más información sobre la creación de aplicaciones y los tipos de implementación, consulte [Create applications](../../apps/deploy-use/create-applications.md) (Crear aplicaciones).  

> [!IMPORTANT]  
>  Puede implementar (instalar/desinstalar) aplicaciones necesarias, pero no paquetes o actualizaciones de software. Los dispositivos móviles tampoco admiten implementaciones simuladas.  
>   
>  Asimismo, los dispositivos móviles no admiten la configuración de programación y experiencia de usuario en el Asistente para implementar software.  

 También puede simular la implementación de una aplicación. Este tipo de implementación prueba la aplicabilidad de una implementación de aplicación en equipos sin instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión** . Para obtener más información, consulte [Simulate application deployments ](../../apps/deploy-use/simulate-application-deployments.md) (Simular implementaciones de aplicaciones).  

## <a name="deploy-an-application"></a>Implementar una aplicación  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la lista de **Aplicaciones** , seleccione la aplicación que desee implementar. A continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.  

4.  En la página **General** del Asistente para implementar software, especifique la información siguiente:  

    -   **Software** : muestra la aplicación para implementar. Puede hacer clic en **Examinar** para seleccionar otra aplicación.  

    -   **Recopilación** : haga clic en **Examinar** para seleccionar la recopilación en la que implementar la aplicación.  

    -   **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación** : seleccione esta opción si desea almacenar el contenido de la aplicación en el grupo de puntos de distribución predeterminados de la recopilación. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción no estará disponible.  

    -   **Distribuir contenido automáticamente para las dependencias** : si esta opción está habilitada y cualquiera de los tipos de implementación de la aplicación contiene dependencias, el contenido de la aplicación dependiente se enviará también a los puntos de distribución.  

        > [!IMPORTANT]  
        >  Si actualiza la aplicación dependiente después de haber implementado la aplicación principal, cualquier contenido nuevo para la dependencia no se distribuirá automáticamente.  

    -   **Comentarios (opcional)** : si lo desea, escriba una descripción de esta implementación.  

5.  En la página **Contenido**, haga clic en **Agregar** para agregar el contenido asociado a esta implementación a los puntos de distribución o grupos de puntos de distribución. Si seleccionó usar puntos de distribución predeterminados asociados a esta recopilación en la página **General**, esta opción se rellenará automáticamente y solo podrá modificarla un miembro del rol de seguridad **Administrador de aplicaciones**.  

6.  Haga clic en **Siguiente**.  

7.  En la página **Configuración de implementación** del Asistente para implementar software, especifique la siguiente información:  

    -   **Acción** : en la lista desplegable, elija si esta implementación está destinada a **Instalar** o **Desinstalar** la aplicación.  

        > [!NOTE]  
        >  Si una aplicación se implementa dos veces en un dispositivo, una vez con una acción de **Instalar** y otra con una acción de **Desinstalar**, la implementación de la aplicación con una acción de **Instalar** tendrá prioridad.  
        >   
        >  No puede cambiar la acción de una implementación después de haberla creado.  

    -   **Propósito** : en la lista desplegable, elija una de las siguientes opciones:  

        -   **Disponible** : si la aplicación se implementa en un usuario, este la verá en el Centro de software y la podrá instalar a petición.  

        -   **Requerido** : la aplicación se implementa automáticamente según la programación configurada. Sin embargo, un usuario puede realizar un seguimiento del estado de la implementación de la aplicación si no está oculto y puede instalar la aplicación antes de la fecha límite desde el Centro de software.  

            > [!NOTE]  
            >  Cuando la acción de implementación se establece en **Desinstalar**, el propósito de la implementación se establece automáticamente en **Requerido** y no se puede cambiar.  

    -   **Implementar automáticamente según la programación tanto si un usuario inició sesión como si no** : si la implementación es en un usuario, seleccione esta opción para implementar la aplicación en los dispositivos primarios del usuario. Esta configuración no requiere que el usuario inicie sesión para ejecutar la implementación. No seleccione esta opción si el usuario debe proporcionar entrada para completar la instalación. Esta opción solo está disponible cuando la implementación tiene un propósito **Requerido**.  

    -   **Enviar paquetes de reactivación** : si el propósito de la implementación se establece en **Requerido** y se selecciona esta opción, se enviará un paquete de reactivación a los equipos antes de instalar la implementación para reactivar el equipo en suspensión a la hora límite de instalación. Para poder utilizar esta opción, los equipos y las redes deben configurarse para Wake on LAN.  

    -   **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales** : esta opción solo está disponible para implementaciones con un propósito **Requerido**.  

    -   **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación** : si esta opción está seleccionada, el administrador debe aprobar las solicitudes de la aplicación de cualquier usuario antes de poder instalarla. Esta opción no está disponible cuando el propósito de la implementación es **Requerido** o cuando se implementa la aplicación en una recopilación de dispositivos.  

        > [!NOTE]  
        >  Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aprobación** , en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** . Si no se aprueba una solicitud de aprobación antes de 45 días, se quitará. Además, volver a instalar el cliente de Configuration Manager puede cancelar las solicitudes de aprobación pendientes.  

    -   **Actualizar automáticamente cualquier versión reemplazada de esta aplicación** : si se selecciona esta opción, cualquier versión reemplazada de la aplicación se actualizará con la aplicación nueva.  

8.  En la página **Programación** del Asistente para implementar software, configure cuándo se implementará o estará disponible para dispositivos clientes esta aplicación.  
    Las opciones de esta página variarán dependiendo de si la acción de la implementación se establece en **Disponible** o **Requerido**.  

9. Si la aplicación que se va a implementar reemplaza a otra aplicación, puede configurar la fecha límite de instalación cuando los usuarios recibirán la nueva aplicación. Haga esto mediante la configuración de **Fecha límite de instalación** para actualizar los usuarios con una aplicación sustituida.  

10. En la página **Experiencia del usuario** del Asistente para implementar software, especifique información sobre cómo pueden interactuar los usuarios con la instalación de la aplicación.
    Cuando implemente aplicaciones en dispositivos de Windows Embedded habilitados para filtro de escritura, puede especificar que se instale la aplicación en la superposición temporal y confirmar los cambios más tarde, o puede confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento. Al confirmar los cambios en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar. Los cambios se conservan en el dispositivo.  
   > [!NOTE]  
   >  Cuando implemente una aplicación en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada. Para obtener más información sobre cómo se usan las ventanas de mantenimiento al implementar aplicaciones en dispositivos de Windows Embedded, consulte el tema [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md) (Crear aplicaciones de Windows Embedded).  
   >  Las opciones **Instalación de software** y **Reinicio del sistema (si es necesario para completar la instalación)** no se usan si el propósito de la implementación está establecido en **Disponible**. También puede configurar el nivel de notificación que ve un usuario cuando se instala la aplicación.  
11. En la página **Alertas** del Asistente para implementar software, configure cómo Configuration Manager y System Center Operations Manager generarán alertas para esta implementación. Puede configurar umbrales para alertas de generación de informes y desactivar los informes durante la implementación.  

12. (Solo para aplicaciones iOS) En la página **Directivas de configuración de la aplicación**, haga clic en **Nuevo** para asociar esta implementación a una directiva de configuración de aplicaciones iOS (si ha creado una). Para obtener más información sobre este tipo de directiva, consulte [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurar aplicaciones iOS con directivas de configuración de aplicaciones).  

13. En la página **Resumen** del Asistente para implementar software, revise las acciones que llevará a cabo esta implementación y, a continuación, haga clic en **Siguiente** para completar el asistente.  

 La nueva implementación se mostrará en la lista de **Implementaciones** en el nodo **Implementaciones** del área de trabajo **Supervisión** . Puede editar las propiedades de esta implementación o eliminar la implementación de la pestaña **Implementaciones** del panel de detalles de la aplicación.  

## <a name="delete-an-application-deployment"></a>Eliminar la implementación de una aplicación  

1.  En la consola de Configuration Manager, haga clic en **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la lista de **Aplicaciones** , seleccione la aplicación cuya implementación se va a eliminar.  

4.  En la pestaña **Implementaciones** de la lista *<nombre de aplicación\>*, seleccione la implementación de la aplicación que desee eliminar. A continuación, en la pestaña **Implementación** , en el grupo **Implementación** , haga clic en **Eliminar**.  

 Cuando se elimina la implementación de una aplicación, no se quitan las instancias de la aplicación que ya se han instalado. Para quitar estas aplicaciones, debe implementar la aplicación en los equipos con la acción **Desinstalar**. Si elimina una implementación de aplicación o quita un recurso de la recopilación en la que está implementando, la aplicación ya no estará visible en el Centro de software.  



<!--HONumber=Nov16_HO1-->


