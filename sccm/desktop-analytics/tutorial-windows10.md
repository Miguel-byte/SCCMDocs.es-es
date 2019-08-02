---
title: 'Tutorial: implementación de Windows 10'
titleSuffix: Configuration Manager
description: Un tutorial sobre el uso de análisis de escritorio y Configuration Manager para implementar Windows 10 en un grupo piloto.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c3e69f2403b3a937c0ad6ba4c913483eb5dfdb1
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712516"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutorial: Implementación de Windows 10 en el piloto

> [!Note]  
> Esta información está relacionada con un servicio de vista previa que se puede modificar sustancialmente antes de que se publique comercialmente. Microsoft no ofrece ninguna garantía, expresa o implícita, con respecto a la información aquí proporcionada.  

En este tutorial se usa análisis de escritorio y Configuration Manager para implementar Windows 10 en un grupo piloto. Resalta la integración del servicio en la nube para proporcionar información sobre la implementación de Windows con el producto local. Use el análisis de escritorio para determinar los mejores dispositivos que se colocarán en un grupo piloto. A continuación, use Configuration Manager para obtener la actual con Windows.

En este tutorial, aprenderá a:  

> [!div class="checklist"]  
> * Configurar el análisis de escritorio en el Azure Portal  
> * Conexión Configuration Manager y configuración del dispositivo  
> * Creación de un plan de implementación de análisis de escritorio para Windows 10  
> * Usar Configuration Manager para implementar Windows 10 en el grupo piloto  

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free) antes de comenzar. Cuando se configura correctamente, el uso de análisis de escritorio no implica ningún costo de Azure.

Análisis de escritorio usa un *área de trabajo de log Analytics* en su suscripción de Azure. Un área de trabajo es esencialmente un contenedor que incluye información de la cuenta e información de configuración sencilla para la cuenta. Para obtener más información, consulte [Administrar áreas de trabajo](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar este tutorial, asegúrese de que tiene los siguientes requisitos previos:  

- Una suscripción de Azure activa, con permisos de [**administrador global**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator)  

    Para obtener más información, consulte [requisitos previos de análisis de escritorio](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, versión 1902 con el paquete acumulativo de actualizaciones (4500571) o posterior, con el rol de **Administrador total**  

- Medios de instalación de la versión más reciente de Windows 10

- Al menos un dispositivo de Windows 10 con las siguientes configuraciones:  

    - Windows 10, versión 1709 o posterior, pero menor que la versión del medio de instalación que piensa usar

    - La actualización más reciente de calidad acumulativa de Windows 10  

    - Configuration Manager la versión de cliente 1902 con el paquete acumulativo de actualizaciones (4500571) o posterior  

- Aprobación empresarial para configurar el nivel de datos de diagnóstico de Windows como **mejorado (limitado)** en los dispositivos piloto  

    Para obtener más información, vea [privacidad de análisis de escritorio](/sccm/desktop-analytics/privacy).

- Conectividad de red desde el dispositivo a los siguientes puntos de conexión de Internet:

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
    - `https://graph.windows.net`(solo en rol de servidor de Configuration Manager)
    - `https://fef.msua06.manage.microsoft.com`(solo en rol de servidor de Configuration Manager)

    Para obtener más información, consulte [habilitación del uso compartido de datos para el análisis de escritorio](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Estos requisitos previos son para los fines de este tutorial. Para obtener más información sobre los requisitos previos generales para el análisis de escritorio con Configuration Manager, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configuración del análisis de escritorio

Use este procedimiento para iniciar sesión en análisis de escritorio y configurarlo en su suscripción. Este procedimiento es un proceso único para configurar el análisis de escritorio de su organización.  

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics) en Microsoft 365 administración de dispositivos como usuario con permisos de **administrador global** . Seleccione **Iniciar**.  

2. En la página **aceptar el contrato de servicio** , revise el contrato de servicio y seleccione **Aceptar**.  

3. En la página **confirmar la suscripción** , la lista de licencias aptas necesarias es para las características de estado de los dispositivos de Windows de análisis de escritorio. Seleccione **Siguiente** para continuar.  

4. En la página **conceder acceso a los usuarios** :

    - **Permita que el análisis de escritorio administre los roles de directorio en su nombre**: El análisis de escritorio asigna automáticamente a los **propietarios del área de trabajo** el rol de **Administrador de análisis de escritorio** . Si esos grupos ya son **administradores globales**, no hay ningún cambio.  

        Si no selecciona esta opción, el análisis de escritorio todavía agrega usuarios como miembros del grupo de seguridad. Un **administrador global** debe asignar manualmente el rol de **Administrador de análisis de escritorio** para los usuarios.  

        Para obtener más información sobre la asignación de permisos de rol de administrador en Azure Active Directory y los permisos asignados a **los administradores de análisis de escritorio**, consulte [permisos de rol de administrador en Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Análisis de escritorio configura previamente el grupo de seguridad **propietarios del área de trabajo** en Azure Active Directory para crear y administrar áreas de trabajo y planes de implementación. 

        Para agregar un usuario al grupo, escriba su nombre o dirección de correo electrónico en la sección **escribir el nombre o la dirección de correo electrónico** . Cuando termine, seleccione **siguiente**.

5. En la página para **configurar el área de trabajo**:  

    > [!Note]  
    > Para completar este paso, el usuario necesita permisos de **propietario del área de trabajo** y acceso adicional a la suscripción y al grupo de recursos de Azure. Para obtener más información, consulte [requisitos previos](/sccm/desktop-analytics/overview#prerequisites).  

    - Seleccione su suscripción de Azure.  

    - Para usar un área de trabajo existente para el análisis de escritorio, selecciónela y continúe con el siguiente paso.  

    - Para crear un área de trabajo para el análisis de escritorio, seleccione **Agregar área de trabajo**.  

        1. Escriba un **nombre de área de trabajo**.  

        2. Seleccione la lista desplegable para **seleccionar el nombre de la suscripción de Azure para esta área de trabajo**y elija la suscripción de Azure para esta área de trabajo.  

        3. **Crear nuevo** Grupo de recursos o **usar existente**.  

        4. Seleccione la **región** en la lista y, a continuación, seleccione **Agregar**.  

6. Seleccione un área de trabajo nueva o existente y, a continuación, seleccione **establecer como área de trabajo de análisis de escritorio**.  Después, seleccione **continuar** en el cuadro de diálogo **confirmar y conceder acceso** .  

7. En la pestaña nuevo explorador, seleccione una cuenta para iniciar sesión. Seleccione la opción para dar **su consentimiento en nombre de su organización** y seleccione **Aceptar**.  


    > [!Note]  
    > Este consentimiento es asignar a la aplicación MALogAnalyticsReader el rol lector Log Analytics para el área de trabajo. El análisis de escritorio requiere este rol de aplicación. Para obtener más información, vea [rol de aplicación MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. De nuevo en la página para **configurar el área de trabajo**, seleccione **siguiente**.  

9. En la página **últimos pasos** , seleccione **ir a análisis de escritorio**. En el Azure Portal se muestra la página **principal** de análisis de escritorio.  



## <a name="connect-configuration-manager"></a>Conexión de Configuration Manager

Use este procedimiento para actualizar Configuration Manager, conectarse a análisis de escritorio y configurar los valores del dispositivo. Este procedimiento es un proceso único para asociar la jerarquía al servicio en la nube.  

### <a name="update-configuration-manager"></a>Actualizar Configuration Manager

Instale el paquete acumulativo de actualizaciones de Configuration Manager versión 1902 (4500571) para admitir la integración con el análisis de escritorio. Para obtener más información sobre esta actualización, vea el [paquete acumulativo de actualizaciones para Configuration Manager rama actual, versión 1902](https://support.microsoft.com/help/4500571).

1. Actualice el sitio con el paquete acumulativo de actualizaciones para la versión 1902. Para más información, vea [Instalar actualizaciones en consola para Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).  

2. Actualice los clientes. Para simplificar el proceso, considere la posibilidad de usar la actualización automática del cliente. Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Conectarse al servicio

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Seleccione **configurar servicios de Azure** en la cinta de opciones.  

2. En la página **servicios de Azure** del Asistente para servicios de Azure, configure las siguientes opciones:  

    - Especifique un **nombre** para el objeto en Configuration Manager  

    - Especifique una **Descripción** opcional que le ayude a identificar el servicio  

    - Seleccione **análisis de escritorio** en la lista de servicios disponibles.  
  
   Seleccione **Next** (Siguiente).  

3. En la página de la **aplicación** , seleccione el **entorno de Azure**adecuado. A continuación, seleccione **examinar** para la aplicación Web.

4. Seleccione **crear** para agregar fácilmente una aplicación Azure ad para la conexión de análisis de escritorio.

5. Configure las siguientes opciones en la ventana **crear aplicación de servidor** :  

    - **Nombre de aplicación**: Un nombre descriptivo para la aplicación en Azure AD.

    - **Dirección URL de la página principal**: Configuration Manager no usa este valor, pero es necesario para Azure AD. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **URI de id. de aplicación**: este valor debe ser único en el inquilino de Azure AD. Está en el token de acceso que usa el cliente de Configuration Manager para solicitar acceso al servicio. De forma predeterminada, este valor es `https://ConfigMgrService`.  

    - **Período de validez de clave secreta**: elija **1 año** o **2 años** en la lista desplegable. El valor predeterminado es un año.  

    Seleccione **iniciar sesión**. Después de autenticarse correctamente en Azure, en la página se muestra el **Nombre de inquilino de Azure AD** como referencia.

    > [!Note]  
    > Complete este paso como **administrador global**. Configuration Manager no guarda estas credenciales. Este rol no requiere permisos de Configuration Manager y no tiene que ser la misma cuenta que ejecuta al Asistente para servicios de Azure.  

    Haga clic en **Aceptar** para crear la aplicación web en Azure AD y cerrar el cuadro de diálogo Crear aplicación de servidor. En el cuadro de diálogo aplicación de servidor, haga clic en **Aceptar**. Después, seleccione **siguiente** en la página aplicación del Asistente para servicios de Azure.  

6. En la página **datos de diagnóstico** , configure las siguientes opciones:  

    - **ID. comercial**: este valor se debe rellenar automáticamente con el identificador de la organización.  

    - **Nivel de datos de diagnóstico de Windows 10**: seleccione al menos **mejorado (limitado)** .  

    - **Permitir el nombre del dispositivo en los datos de diagnóstico**: seleccione **Habilitar** .  
  
   Seleccione **Next** (Siguiente). La página **funcionalidad disponible** muestra la funcionalidad de análisis de escritorio que está disponible con la configuración de datos de diagnóstico de la página anterior. Seleccione **Next** (Siguiente).  

7. En la página **colecciones** , configure las siguientes opciones:  

    - **Nombre para mostrar**: El portal de análisis de escritorio muestra esta conexión Configuration Manager con este nombre. Úselo para diferenciar entre diferentes jerarquías. Por ejemplo, *laboratorio de pruebas* o *producción*.  

    - **Recopilación de destino**: Esta colección incluye todos los dispositivos que Configuration Manager configura con el identificador comercial y la configuración de datos de diagnóstico. Es el conjunto completo de dispositivos que Configuration Manager se conecta al servicio de análisis de escritorio.  

    - **Los dispositivos de la recopilación de destino usan un proxy autenticado por el usuario para la comunicación saliente**: De forma predeterminada, este valor es **no**. Si es necesario en su entorno, establezca en **sí**.  

    - **Seleccione recopilaciones específicas para sincronizar con el análisis de escritorio**: Seleccione **Agregar** para incluir colecciones adicionales. Estas colecciones están disponibles en el portal de análisis de escritorio para agrupar con planes de implementación. Asegúrese de incluir recopilaciones piloto y de exclusión piloto.  

        Estas colecciones continúan sincronizando a medida que cambian sus pertenencias. Por ejemplo, el plan de implementación utiliza una recopilación con una regla de pertenencia de Windows 7. Cuando esos dispositivos se actualizan a Windows 10 y Configuration Manager evalúa la pertenencia a la recopilación, dichos dispositivos salen de la colección y del plan de implementación.  

8. Complete el asistente.  

Configuration Manager crea una directiva de configuración para configurar los dispositivos de la recopilación de destino. Esta directiva incluye la configuración de datos de diagnóstico para permitir que los dispositivos envíen datos a Microsoft. De forma predeterminada, los clientes actualizan la Directiva cada hora. Después de recibir la nueva configuración, pueden transcurrir varias horas antes de que los datos estén disponibles en el análisis de escritorio.

> [!Note]  
> Para obtener más información sobre esta configuración, vea [configuración de Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Supervise la configuración de los dispositivos para el análisis de escritorio. En la consola de Configuration Manager, vaya al área de trabajo **biblioteca de software** , expanda el nodo servicio de **análisis de escritorio** y seleccione el panel estado de la **conexión** .  

Configuration Manager sincroniza las colecciones en un plazo de 60 minutos a partir de la creación de la conexión. En el portal de análisis de escritorio, vaya a **proyecto piloto global**y vea las colecciones de dispositivos Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Creación de un plan de implementación de análisis de escritorio

Use este procedimiento para crear un plan de implementación en análisis de escritorio.

1. Abra el [portal de análisis de escritorio](https://aka.ms/desktopanalytics). Use credenciales que tengan, como mínimo, permisos de **colaborador del área de trabajo** .  

2. Seleccione **planes de implementación** en el grupo administrar.  

3. En el panel **planes de implementación** , seleccione **crear**.  

4. En el panel **crear plan de implementación** , configure las siguientes opciones:  

    - **Nombre**: Un nombre único para el plan de implementación, por ejemplo`Windows 10 pilot`  

    - **Productos y versiones**: Seleccione el producto de **Windows** y la versión recomendada más reciente disponible. Por ejemplo, **Windows 10, versión 1809 (recomendado)** .  

    - **Grupos de dispositivos**: Seleccione uno o varios grupos en la pestaña Configuration Manager y, a continuación, seleccione **establecer como grupos de destino**. Estos grupos son recopilaciones sincronizadas desde Configuration Manager.  

    - **Reglas de preparación**: Estas reglas ayudan a determinar qué dispositivos son aptos para la actualización. Seleccione **sistema operativo Windows** y configure las siguientes opciones:  

        - **Mis equipos obtienen automáticamente controladores de Windows Update**: La configuración predeterminada es **OFF**, que se recomienda al implementar con Configuration Manager.  

        - **Defina un umbral de recuento de instalaciones bajo para las aplicaciones**: El valor predeterminado es `2%`. Las aplicaciones por debajo de este umbral se establecen automáticamente en el recuento de *instalaciones bajas*. El análisis de escritorio no valida estos complementos durante el programa piloto.  

            Si una aplicación se instala en un porcentaje mayor de equipos que este umbral, el plan de implementación marca la aplicación como *digno*de interés. Después, puede decidir su importancia para probarla durante la fase piloto.  

    - **Fecha**de finalización: Elija la fecha en que Windows debe implementarse completamente en todos los dispositivos de destino.  

5. Seleccione **Crear**. El nuevo plan aparece en la lista de planes de implementación mientras se está procesando. Para agilizar el procesamiento, solicite una actualización de datos a petición. Para obtener más información, consulte [p + f de análisis de escritorio](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Abra el plan de implementación seleccionando su nombre.  

7. En el menú plan de implementación, en el grupo **preparar** , seleccione **identificar importancia**.  

    1. En la pestaña **aplicaciones** , seleccione Mostrar solo los activos **no** revisados.  

    2. Seleccione cada aplicación y, a continuación, seleccione **Editar**. Puede seleccionar más de una aplicación para editarla al mismo tiempo.  

    3. Elija un nivel de importancia de la lista **importancia** . Si quiere que el análisis de escritorio valide la aplicación durante la prueba piloto, seleccione **crítico** o **importante**. No valida las aplicaciones marcadas como **no importantes**. Evalúe su [compatibilidad](/sccm/desktop-analytics/compat-assessment) y otros detalles del plan al asignar niveles de importancia.  

        Al asignar niveles de importancia, también puede elegir la decisión de actualización.  

    4. Cuando haya terminado, seleccione **Guardar** .  

8. En el menú plan de implementación, en el grupo **preparar** , seleccione **identificar piloto**.  

    1. Revise los dispositivos recomendados para la prueba piloto.  

    2. Seleccione cada dispositivo y seleccione **Agregar a piloto**. Si no está de acuerdo con la recomendación, seleccione **reemplazar**.  

        Para obtener más información sobre cómo Desktop Analytics realiza estas recomendaciones, seleccione el icono de información en la esquina superior derecha del panel **identificar piloto** .



## <a name="deploy-windows-10-in-configuration-manager"></a>Implementación de Windows 10 en Configuration Manager

Use este procedimiento para implementar Windows 10 en Configuration Manager al grupo piloto.

- Si aún no tiene una, cree primero [un paquete de actualización del sistema operativo para Windows 10](#bkmk_create-package) .  

- Si aún no tiene una, [cree una secuencia de tareas de actualización del sistema operativo para Windows 10](#bkmk_create-ts) .  

- [Implementación de la secuencia de tareas](#bkmk_deploy-ts) mediante el plan de implementación de análisis de escritorio  

- [Instalación de la secuencia de tareas desde el](#bkmk_install-ts) centro de software en un dispositivo de destino  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a>Crear un paquete de actualización del sistema operativo para Windows 10

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y después haga clic en el nodo **Paquetes de actualización del sistema operativo**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **Crear**, haga clic en **Agregar paquete de actualización de sistema operativo**. Esta acción inicia el asistente para agregar una actualización del sistema operativo.  

3. En la página **origen de datos** , especifique la **ruta de acceso** de red a los archivos de origen de instalación del paquete de actualización del sistema operativo. Por ejemplo, `\\server\share\path`.  

    > [!NOTE]  
    > Los archivos de origen de instalación contienen setup.exe y otros archivos y carpetas para instalar el sistema operativo.  

4. En la página **General** , especifique un **nombre** único para el paquete de actualización del sistema operativo.  

5. Complete el Asistente para agregar paquete de actualización de sistema operativo.  

#### <a name="distribute-content"></a>Distribución de contenido

A continuación, distribuya el paquete de actualización del sistema operativo a puntos de distribución.  

1. Seleccione el paquete de actualización del sistema operativo en la lista. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Distribuir contenido**. Se abre el Asistente para distribuir contenido.  

2. En la página **General** , compruebe que el contenido que aparece es el contenido que desea distribuir y, a continuación, seleccione **siguiente**.  

3. En la página **destino del contenido** , seleccione **Agregar**y elija **punto de distribución**. Seleccione un punto de distribución existente y, a continuación, haga clic en **Aceptar**. Cuando termine de agregar los destinos de contenido, seleccione **siguiente**.  

4. Complete el Asistente para distribuir contenido.  


### <a name="bkmk_create-ts"></a>Creación de una secuencia de tareas de actualización del sistema operativo para Windows 10

1. En la consola de Configuration Manager, vaya al área de trabajo **biblioteca de software** , expanda **sistemas operativos**y, a continuación, seleccione **secuencias de tareas**.  

2. En la pestaña **Inicio** de la cinta de opciones, en el grupo **crear** , seleccione **crear secuencia de tareas**.  

3. En la página **crear una nueva secuencia de tareas** del Asistente para crear secuencia de tareas, seleccione **actualizar un sistema operativo desde un paquete de actualización**y, después, seleccione **siguiente**.  

4. En la página **información de secuencia de tareas** , especifique un nombre de secuencia de **tareas** que identifique la secuencia de tareas.  

5. En la página **actualizar el sistema operativo Windows** , especifique la siguiente configuración y, a continuación, seleccione **siguiente**:  

    - **Paquete de actualización**: especifique el paquete de actualización que contenga los archivos de origen de actualización del sistema operativo.  

    - **Índice de ediciones**: si hay varios índices de edición del sistema operativo disponibles en el paquete, seleccione el índice de la edición deseada. De forma predeterminada, el asistente selecciona el primer índice.  

    - **Clave de producto**: especifique la clave de producto de Windows para el sistema operativo que quiera instalar. Puede especificar claves de licencia por volumen codificadas o claves de producto estándar. Si usa una clave de producto estándar, separe cada grupo de cinco caracteres por un guion (-). Por ejemplo:  *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Si se trata de una actualización de una edición de licencia por volumen, la clave de producto puede no ser necesaria.  

        > [!Note]  
        > Esta clave de producto puede ser una clave de activación múltiple (CAM) o una clave de licencias por volumen genérica (CLVG). Las CLVG también se conocen como claves de configuración de cliente del servicio de administración de claves (SAC). Para obtener más información, consulte [Plan para la activación por volumen](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Para obtener una lista de claves de configuración de cliente KMS, consulte el [Apéndice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) de la Guía de activación de Windows Server.

6. En la página **incluir actualizaciones** , seleccione **siguiente** para no instalar ninguna actualización de software.  

7. En la página **instalar aplicaciones** , seleccione **siguiente** para no instalar ninguna aplicación.

8. Complete el Asistente para crear secuencia de tareas.  


### <a name="bkmk_deploy-ts"></a>Implementación de la secuencia de tareas mediante el plan de implementación de análisis de escritorio

1. En la consola de Configuration Manager, vaya a la **biblioteca de software**, expanda servicios de análisis de **escritorio**y seleccione el nodo planes de **implementación** .  

2. Seleccione el plan de implementación piloto de Windows 10 y, después, seleccione **detalles del plan de implementación** en la cinta de opciones.  

3. En el icono **Estado piloto** , elija **secuencia de tareas** en la lista desplegable y, a continuación, seleccione **implementar**.  

4. En la página **General** del Asistente para implementar software, seleccione **examinar** junto al campo **software** . Seleccione la secuencia de tareas de actualización en contexto de Windows 10 y seleccione **siguiente**.  

    > [!Note]  
    > Con la integración de análisis de escritorio, Configuration Manager crea automáticamente colecciones piloto y de producción para el plan de implementación. Antes de poder usarlas, puede tardar tiempo en sincronizarse estas colecciones. Para obtener más información, consulte [solución de problemas: latencia de datos](/sccm/desktop-analytics/troubleshooting#data-latency).<!-- 4984639 -->
    >
    > Esta colección está reservada para los dispositivos del plan de implementación de análisis de escritorio. No se admiten cambios manuales en esta colección.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. En la página **contenido** , seleccione **Agregar**y, a continuación, seleccione **punto de distribución**. Seleccione un punto de distribución disponible para hospedar el contenido de instalación y seleccione **Aceptar**. A continuación, seleccione **Siguiente**.  

6. En la página **configuración de implementación** , seleccione **siguiente** para aceptar la configuración predeterminada. (Una instalación disponible).  

7. En la página **programación** , seleccione **siguiente** para aceptar la configuración predeterminada. (Disponible lo antes posible).  

8. En la página **experiencia del usuario** , seleccione **siguiente** para aceptar la configuración predeterminada. (Mostrar en el centro de software y mostrar solo notificaciones para los reinicios del equipo).  

9. En la página **alertas** , seleccione **siguiente** para aceptar la configuración predeterminada.  

10. Complete el asistente.  


### <a name="bkmk_install-ts"></a>Instalación de la secuencia de tareas desde el centro de software

1. Inicie sesión en un dispositivo que sea miembro del plan de implementación piloto.  

2. Abra el **centro de software** e instale el sistema operativo disponible para Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Pasos siguientes

Continúe con el siguiente artículo para obtener más información sobre los planes de implementación de análisis de escritorio.
> [!div class="nextstepaction"]  
> [Planes de implementación](/sccm/desktop-analytics/about-deployment-plans)
