---
title: 'Tutorial: implementar Windows 10'
titleSuffix: Configuration Manager
description: Un tutorial sobre el uso de escritorio de análisis y Configuration Manager para implementar Windows 10 en un grupo piloto.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d564a5161011a1af0a4ec70f9bf7b45d87dd9dcb
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623163"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Implementación de Windows 10 en el piloto

> [!Note]  
> Esta información se relaciona con un servicio en versión preliminar que puede modificarse sustancialmente antes de su lanzamiento comercial. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

Este tutorial usa el escritorio de análisis y Configuration Manager para implementar Windows 10 en un grupo piloto. Resalta la integración del servicio de nube para ofrecer información para implementar Windows con el producto local. Use escritorio análisis para determinar los dispositivos que mejor se pone en un grupo piloto. A continuación, use Configuration Manager para obtener actual con Windows.

En este tutorial, obtendrá información sobre cómo:  

> [!div class="checklist"]  
> * Configurar análisis de escritorio en el portal de Azure  
> * Conectar Configuration Manager y la configuración de dispositivos  
> * Crear un plan de implementación de análisis de escritorio para Windows 10  
> * Use el Administrador de configuración para implementar Windows 10 en el grupo piloto  

Si no tiene una suscripción de Azure, cree un [cuenta gratuita](https://azure.microsoft.com/free) antes de comenzar. Cuando se configuran correctamente, uso de análisis de escritorio no incurrir en ningún gasto de Azure.

Análisis de escritorio usa un *área de trabajo de Log Analytics* en su suscripción de Azure. Un área de trabajo es básicamente un contenedor que incluye información de la cuenta y la información de configuración sencilla para la cuenta. Para obtener más información, consulte [Administrar áreas de trabajo](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Requisitos previos

Antes de empezar este tutorial, asegúrese de que tiene los siguientes requisitos previos:  

- Una suscripción activa de Azure, con [ **administrador Global** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) permisos  

    Para obtener más información, consulte [requisitos previos de análisis de escritorio](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, versión 1902 con paquete acumulativo de actualizaciones (4500571) o posterior, con **Administrador total** rol  

- Medios de instalación para la versión más reciente de Windows 10

- Al menos un dispositivo Windows 10 con las siguientes configuraciones:  

    - Windows 10, versión 1709 o versiones posterior, pero menor que la versión de los medios de instalación que se va a usar

    - La última actualización acumulativa de calidad de Windows 10  

    - La versión de cliente 1902 Configuration Manager con paquete acumulativo de actualizaciones (4500571) o posterior  

- Aprobación de la empresa para configurar el nivel de datos de diagnóstico de Windows para **mejorado (limitado)** en los dispositivos pilotos  

    Para obtener más información, consulte [privacidad escritorio Analytics](/sccm/desktop-analytics/privacy).

- Conectividad de red del dispositivo con los siguientes puntos de conexión de internet:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (en Configuration Manager solo rol de servidor)
    - `https://fef.msua06.manage.microsoft.com` (en Configuration Manager solo rol de servidor)

    Para obtener más información, consulte [cómo habilitar el uso compartido para el escritorio de análisis de datos](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estos requisitos previos son para los fines de este tutorial. Para obtener más información sobre los requisitos previos generales para el análisis de escritorio con Configuration Manager, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configuración del análisis de escritorio

Utilice este procedimiento para iniciar sesión el análisis de escritorio y configurarlo en su suscripción. Este procedimiento es un proceso único para configurar los análisis de escritorio de su organización.  

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) en administración de dispositivos de Microsoft 365 como un usuario con **administrador Global** permisos. Seleccione **iniciar**.  Si se le solicitará un código de invitación, use: `DesktopAnalyticsRocks!`

2. En el **acepte el contrato de servicio** página, revise el contrato de servicio y seleccione **Accept**.  

3. En el **confirmar la suscripción** página, la lista de licencias aplicables necesarias son para las características del estado de dispositivos de Windows de análisis de escritorio. Seleccione **Siguiente** para continuar.  

4. En el **dar acceso a los usuarios** página:

    - **Permitir análisis de escritorio para administrar roles de directorio en su nombre**: Escritorio Analytics asigna automáticamente el **propietarios del área de trabajo** el **Desktop Analytics Administrator** rol. Si esos grupos ya están un **administrador Global**, no hay ningún cambio.  

        Si no selecciona esta opción, análisis de escritorio seguirá agregando los usuarios como miembros del grupo de seguridad. Un **administrador Global** debe asignar manualmente el **Desktop Analytics Administrator** rol para los usuarios.  

        Para obtener más información acerca de cómo asignar permisos del rol de administrador en Azure Active Directory y los permisos asignados a **Desktop Analytics administradores**, consulte [permisos del rol de administrador en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis escritorio preconfigura la **propietarios del área de trabajo** grupo de seguridad en Azure Active Directory para crear y administrar áreas de trabajo y los planes de implementación. 

        Para agregar un usuario al grupo, escriba su dirección de correo electrónico o de nombre en el **escriba la dirección de correo electrónico o nombre** sección. Cuando termine, seleccione **siguiente**.

5. En la página para **configurar el área de trabajo**:  

    > [!Note]  
    > Para completar este paso, el usuario debe **propietario del área de trabajo** permisos y acceso adicional a la suscripción de Azure y el grupo de recursos. Para obtener más información, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  

    - Seleccione su suscripción de Azure.  

    - Para usar un área de trabajo para el análisis de escritorio, selecciónela y continúe con el paso siguiente.  

    - Para crear un área de trabajo para el análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo**.  

        2. Seleccione la lista desplegable para **seleccione el nombre de la suscripción de Azure para esta área de trabajo**y elija la suscripción de Azure para esta área de trabajo.  

        3. **Crear nuevo** grupo de recursos o **usar existente**.  

        4. Seleccione el **región** en la lista y, a continuación, seleccione **agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **establecer como área de trabajo de análisis de escritorio**.  A continuación, seleccione **continuar** en el **confirmar y concederle acceso** cuadro de diálogo.  

7. En la nueva pestaña del explorador, elija una cuenta para que use para iniciar sesión. Seleccione la opción de **dar su consentimiento en nombre de su organización** y seleccione **Accept**.  


    > [!Note]  
    > Este consentimiento consiste en asignar el rol de lector de Log Analytics para el área de trabajo de la aplicación de MALogAnalyticsReader. Este rol de aplicación es necesario por el análisis de escritorio. Para obtener más información, consulte [rol de aplicación MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. En la página a **configurar el área de trabajo**, seleccione **siguiente**.  

9. En el **últimos pasos** página, seleccione **vaya al escritorio Analytics**. El portal de Azure muestra el análisis de escritorio **inicio** página.  



## <a name="connect-configuration-manager"></a>Conexión de Configuration Manager

Utilice este procedimiento para actualizar Configuration Manager, conexión a escritorio Analytics y configuración de dispositivos. Este procedimiento es un proceso único para asociar la jerarquía para el servicio en la nube.  

### <a name="update-configuration-manager"></a>Actualizar Configuration Manager

Instale el paquete de actualizaciones de Configuration Manager versión 1902 (4500571) para admitir la integración con análisis de escritorio. Para obtener más información sobre esta actualización, consulte [acumulativo de actualizaciones de la rama actual de Configuration Manager, versión 1902](https://support.microsoft.com/help/4500571).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conectarse al servicio

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

2. En el **Azure Services** página del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **nombre** para el objeto en Configuration Manager  

    - Especificar un elemento opcional **descripción** para ayudarle a identificar el servicio  

    - Seleccione **Desktop Analytics** en la lista de servicios disponibles  
  
   Seleccione **Siguiente**.  

3. En el **aplicación** , seleccione la adecuada **entorno Azure**. A continuación, seleccione **examinar** para la aplicación web.

4. Seleccione **crear** agregar fácilmente una aplicación de Azure AD para la conexión de escritorio Analytics.

5. Configure las siguientes opciones en el **crear aplicación de servidor** ventana:  

    - **Nombre de aplicación**: Un nombre descriptivo para la aplicación en Azure AD.

    - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. En el token de acceso sirve por el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.  

    Seleccione **inicie sesión en**. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

    > [!Note]  
    > Completar este paso como una **administrador Global**. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.  

    Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. En el cuadro de diálogo de la aplicación de servidor, seleccione **Aceptar**. A continuación, seleccione **siguiente** en la página de aplicación del Asistente para servicios de Azure.  

6. En el **datos de diagnóstico** página, configure las opciones siguientes:  

    - **Id. comercial**: este valor se debería rellenar automáticamente con el ID de. su organización  

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **mejorado (limitado)**  

    - **Permitir que el nombre del dispositivo en los datos de diagnóstico**: seleccione **habilitar**  
  
   Seleccione **Siguiente**. El **funcionalidad disponible** página muestra la funcionalidad de análisis de escritorio que está disponible con la configuración de datos de diagnóstico desde la página anterior. Seleccione **Siguiente**.  

7. En el **colecciones** página, configure las opciones siguientes:  

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión de Configuration Manager con este nombre. Puede usarlo para diferenciar entre jerarquías diferentes. Por ejemplo, *laboratorio de pruebas* o *producción*.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos de Configuration Manager se configura con el Id. comercial y la configuración de datos de diagnóstico. Es el conjunto completo de los dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usa un proxy de usuario autenticado para la comunicación saliente**: De forma predeterminada, este valor es **No**. Si es necesario en su entorno, se establece en **Sí**.  

    - **Seleccione las recopilaciones específicas para sincronizar con análisis de escritorio**: Seleccione **agregar** para incluir las colecciones adicionales. Estas colecciones están disponibles en el portal de análisis de escritorio para su agrupación con planes de implementación. No olvide incluir colecciones de exclusión de pruebas y pruebas.  

        Estas colecciones continuarán con la sincronización como sus cambios de pertenencia. Por ejemplo, el plan de implementación usa una colección con una regla de pertenencia a Windows 7. Como esos dispositivos se actualización a Windows 10 y Configuration Manager evalúa la pertenencia a recopilación, quitar esos dispositivos fuera de la recopilación y el plan de implementación.  

8. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos en la colección de destino. Esta directiva incluye la configuración de datos de diagnóstico para habilitar dispositivos para enviar datos a Microsoft. De forma predeterminada, los clientes actualizan la directiva cada hora. Después de recibir la nueva configuración, puede ser más varias horas antes de que los datos están disponibles en análisis de escritorio.

> [!Note]  
> Para obtener más información sobre estas opciones, consulte [configuración Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Supervisar la configuración de los dispositivos para el análisis de escritorio. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda el **escritorio Analytics mantenimiento** nodo y seleccione el **estado de conexión** panel.  

Configuration Manager sincroniza las colecciones dentro de 60 minutos después de crear la conexión. En el portal de análisis de escritorio, vaya a **piloto Global**y ver las colecciones de dispositivos de Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Crear un plan de implementación de análisis de escritorio

Utilice este procedimiento para crear un plan de implementación en escritorio Analytics.

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics). Use las credenciales que tienen al menos **colaboradores del área de trabajo** permisos.  

2. Seleccione **planes de implementación** en el grupo de administración.  

3. En el **planes de implementación** panel, seleccione **crear**.  

4. En el **Crear plan de implementación** panel, configure las siguientes opciones:  

    - **Nombre**: Planear un nombre único para la implementación, por ejemplo `Windows 10 pilot`  

    - **Productos y versiones**: Seleccione el **Windows** producto y la versión recomendada más reciente disponible. Por ejemplo, **Windows 10, versión 1809 (recomendado)** .  

    - **Grupos de dispositivos**: Seleccione uno o más grupos en la pestaña de Configuration Manager y, a continuación, seleccione **establecer como destino grupos**. Estos grupos son recopilaciones sincronizadas desde Configuration Manager.  

    - **Las reglas de preparación**: Estas reglas ayudan a determinar qué dispositivos necesarios para actualización. Seleccione **del sistema operativo WIndows** y configure las siguientes opciones:  

        - **Mis equipos obtienen automáticamente los controladores de Windows Update**: El valor predeterminado es **desactivar**, que es el recomendado al implementar con Configuration Manager.  

        - **Definir un umbral de recuento de baja de instalación para las aplicaciones**: El valor predeterminado es `2%`. Las aplicaciones por debajo del umbral se establecen automáticamente en *bajo número de instalaciones*. Análisis de escritorio no validación estos complementos durante la prueba piloto.  

            Si una aplicación está instalada en un mayor porcentaje de equipos a este umbral, el plan de implementación marca la aplicación como *Noteworthy*. A continuación, puede decidir su importancia para la prueba durante la fase piloto.  

    - **Fecha de finalización**: Elija la fecha por el que se deberían implementar totalmente Windows en todos los dispositivos de destino.  

5. Seleccione **Crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Para acelerar el procesamiento, solicitar una actualización de datos y a petición. Para obtener más información, consulte [preguntas más frecuentes sobre análisis de escritorio](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Abrir el plan de implementación, seleccione su nombre.  

7. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar importancia**.  

    1. En el **aplicaciones** pestaña, seleccione esta opción para mostrar sólo **no revisado** activos.  

    2. Seleccione cada aplicación y, a continuación, seleccione **editar**. Puede seleccionar más de una aplicación para editar al mismo tiempo.  

    3. Elija un nivel de importancia de la **importancia** lista. Si desea que el análisis de escritorio para validar la aplicación durante el programa piloto, seleccione **crítico** o **importante**. No valida las aplicaciones marcadas como **importante no**. Evalúe su [compatibilidad](/sccm/desktop-analytics/compat-assessment) y otra información del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Seleccione **guardar** cuando haya terminado.  

8. En el menú del plan de implementación, en el **preparar** grupo, seleccione **identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **agregar piloto**. Si no está de acuerdo con la recomendación, seleccione **reemplazar**.  

        Para obtener más información sobre cómo escritorio Analytics hace que estas recomendaciones, seleccione el icono de información en la esquina superior derecha de la **identificar piloto** panel.



## <a name="deploy-windows-10-in-configuration-manager"></a>Implementar Windows 10 en Configuration Manager

Utilice este procedimiento para implementar Windows 10 en Configuration Manager en el grupo piloto.

- Si aún no tiene uno, en primer lugar [crear un paquete de actualización del sistema operativo para Windows 10](#bkmk_create-package)  

- Si aún no tiene una, [crear una secuencia de tareas de actualización del sistema operativo para Windows 10](#bkmk_create-ts)  

- [Implementar la secuencia de tareas](#bkmk_deploy-ts) con el plan de implementación de análisis de escritorio  

- [Instale la secuencia de tareas](#bkmk_install-ts) desde el centro de Software en un dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a> Crear un paquete de actualización del sistema operativo para Windows 10

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Paquetes de actualización del sistema operativo**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar paquete de actualización de sistema operativo**. Esta acción inicia el asistente para agregar una actualización del sistema operativo.  

3. En el **origen de datos** , especifique la red **ruta** a la instalación de archivos de código fuente del sistema operativo actualizan el paquete. Por ejemplo: `\\server\share\path`.  

    > [!NOTE]  
    > Los archivos de origen de instalación contienen setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

4. En el **General** , especifique un único **nombre** paquete de actualización para el sistema operativo.  

5. Complete el Asistente para paquete de actualización de sistema operativo agregar.  

#### <a name="distribute-content"></a>Distribución de contenido

A continuación, distribuya el paquete de actualización del sistema operativo a puntos de distribución.  

1. Seleccione el paquete de actualización del sistema operativo en la lista. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Distribuir contenido**. Se abre el Asistente para distribuir contenido.  

2. En el **General** , comprueba que el contenido que aparece es el contenido que desea distribuir y, a continuación, seleccione **siguiente**.  

3. En el **destino del contenido** página, seleccione **agregar**y elija **punto de distribución**. Seleccione un punto de distribución existente y, a continuación, seleccione **Aceptar**. Cuando termine de agregar los destinos del contenido, seleccione **siguiente**.  

4. Complete el Asistente para distribuir contenido.  


### <a name="bkmk_create-ts"></a> Crear una secuencia de tareas de actualización del sistema operativo para Windows 10

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software** área de trabajo, expanda **sistemas operativos**y, a continuación, seleccione **secuencias de tareas**.  

2. En el **inicio** pestaña de la cinta de opciones, en el **crear** grupo, seleccione **crear secuencia de tareas**.  

3. En el **crear nueva secuencia de tareas** página de la secuencia de Asistente para crear tareas, seleccione **actualizar un sistema operativo desde un paquete de actualización**y, a continuación, seleccione **siguiente**.  

4. En el **información de secuencia de tareas** , especifique un **nombre de la secuencia de tareas** que identifica la secuencia de tareas.  

5. En el **actualizar el sistema operativo Windows** , especifique las siguientes opciones y, a continuación, seleccione **siguiente**:  

    - **Paquete de actualización**: especifique el paquete de actualización que contenga los archivos de origen de actualización del sistema operativo.  

    - **Índice de ediciones**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, el asistente selecciona el primer índice.  

    - **Clave de producto**: especifique la clave de producto de Windows para el sistema operativo que quiera instalar. Puede especificar claves de licencia por volumen codificadas o claves de producto estándar. Si usa una clave de producto estándar, separe cada grupo de cinco caracteres por un guion (-). Por ejemplo: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto puede no ser necesaria.  

        > [!Note]  
        > Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server.

6. En el **incluir actualizaciones** página, seleccione **siguiente** no instalar ningún software de las actualizaciones.  

7. En el **instalar aplicaciones** página, seleccione **siguiente** no instalar ninguna aplicación.

8. Complete el Asistente para la secuencia de tareas de crear.  


### <a name="bkmk_deploy-ts"></a> Implementar la secuencia de tareas con el plan de implementación de análisis de escritorio

1. En la consola de Configuration Manager, vaya a la **biblioteca de Software**, expanda **Desktop Analytics mantenimiento**y seleccione el **planes de implementación** nodo.  

2. Seleccione el plan de implementación piloto de Windows 10 y, a continuación, seleccione **detalles del Plan de implementación** en la cinta de opciones.  

3. En el **piloto estado** icono, elija **secuencia de tareas** desde la lista desplegable y, a continuación, seleccione **implementar**.  

4. En el **General** página del Asistente para implementar Software, seleccione **examinar** junto a la **Software** campo. Seleccione la secuencia de tareas de actualización en contexto de Windows 10 y seleccione **siguiente**.  

    > [!Note]  
    > Con la integración de análisis de escritorio, Configuration Manager crea automáticamente una colección para el plan de implementación piloto. Puede tardar hasta 10 minutos para sincronizar antes de que se puede usar esta colección.<!-- 3887891 -->
    >
    > Esta colección está reservada para los dispositivos de plan de implementación de escritorio Analytics. No se admiten los cambios manuales a esta colección.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. En el **contenido** página, seleccione **agregar**y, a continuación, seleccione **punto de distribución**. Seleccione un punto de distribución disponibles para hospedar el contenido de instalación y seleccione **Aceptar**. A continuación, seleccione **Siguiente**.  

6. En el **configuración de implementación** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Una instalación disponible).  

7. En el **programación** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Disponible tan pronto como sea posible).  

8. En el **experiencia del usuario** página, seleccione **siguiente** para aceptar la configuración predeterminada. (Mostrar en el centro de Software y mostrar solo las notificaciones para reinicios del equipo).  

9. En el **alertas** página, seleccione **siguiente** para aceptar la configuración predeterminada.  

10. Complete el asistente.  


### <a name="bkmk_install-ts"></a> Instalar la secuencia de tareas desde el centro de Software

1. Inicie sesión en un dispositivo que sea miembro del plan de implementación piloto.  

2. Abra **centro de Software** e instalar el sistema operativo disponible para Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para obtener más información sobre los planes de implementación de análisis de escritorio.
> [!div class="nextstepaction"]  
> [Planes de implementación](/sccm/desktop-analytics/about-deployment-plans)
