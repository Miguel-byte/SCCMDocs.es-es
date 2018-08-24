---
title: Implementar aplicaciones
titleSuffix: Configuration Manager
description: Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d23c5ee5b81264a9725c4654cd1717b30302c708
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384827"
---
# <a name="deploy-applications-with-configuration-manager"></a>Implementar aplicaciones con Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario en Configuration Manager. Esta implementación proporciona instrucciones para el cliente de Configuration Manager sobre cómo y cuándo instalar el software. 

Antes de implementar una aplicación, cree al menos un tipo de implementación para la aplicación. Para obtener más información, consulte [Create applications](/sccm/apps/deploy-use/create-applications) (Creación de aplicaciones).

También puede simular la implementación de una aplicación. Esta simulación prueba la aplicabilidad de una implementación sin instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión**. Para obtener más información, consulte el artículo sobre [simular implementaciones de aplicaciones ](/sccm/apps/deploy-use/simulate-application-deployments).

> [!Note]
>  Solo se puede simular la implementación de las aplicaciones obligatorias, pero no se pueden simular paquetes ni actualizaciones de software.   
> 
>  Los dispositivos inscritos en MDM no admiten las implementaciones simuladas, la experiencia del usuario o la configuración de programación.



## <a name="bkmk_deploy"></a> Implementar una aplicación

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2.  En la lista **Aplicaciones**, seleccione la aplicación que quiera implementar. En la cinta de opciones, haga clic en **Implementar**.  

> [!Note]  
> Al ver las propiedades de una implementación existente, las secciones siguientes se corresponden con pestañas de la ventana de propiedades de la implementación:  
> - [General](#bkmk_deploy-general)
> - [Contenido](#bkmk_deploy-content)
> - [Configuración de implementación](#bkmk_deploy-settings)
> - [Programación](#bkmk_deploy-sched)
> - [Experiencia del usuario](#bkmk_deploy-ux)
> - [Alertas](#bkmk_deploy-alerts)
> - [iOS: Directivas de configuración de aplicaciones](#bkmk_deploy-ios)


### <a name="bkmk_deploy-general"></a> Información **general** sobre implementaciones 

En la página **General** del Asistente para implementar software, especifique la información siguiente:  

- **Software**: este valor muestra la aplicación que se va a implementar. Haga clic en **Examinar** para seleccionar otra aplicación.  

- **Recopilación**: haga clic en **Examinar** para seleccionar la recopilación en la que se va a implementar la aplicación.  

- **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: almacene el contenido de la aplicación en el grupo de puntos de distribución predeterminado de la recopilación. Si no ha asociado la colección seleccionada a un grupo de puntos de distribución, esta opción estará atenuada.  

- **Distribuir contenido automáticamente para las dependencias**: si alguno de los tipos de implementación de la aplicación tiene dependencias, el sitio también enviará contenido de aplicaciones dependientes a los puntos de distribución.  

    >[!Note]  
    > Si actualiza la aplicación dependiente después de implementar la aplicación principal, el sitio no distribuye automáticamente ningún contenido nuevo para la dependencia.  

- **Comentarios (opcional)**: si quiere, escriba una descripción para esta implementación.  


### <a name="bkmk_deploy-content"></a> Opciones de **contenido** de implementación

En la página **Contenido**, haga clic en **Agregar** para distribuir el contenido para esta aplicación a un punto de distribución o a un grupo de puntos de distribución. 

Si ha seleccionado la opción **Usar puntos de distribución predeterminados asociados a esta colección** en la página General, esta opción estará rellenada automáticamente. Solo un miembro del rol de seguridad **Administrador de aplicaciones** puede modificarla.

Si el contenido de aplicaciones ya se ha distribuido, se mostrará aquí. 


### <a name="bkmk_deploy-settings"></a> **Configuración de implementación**

En la página **Configuración de implementación**, especifique la siguiente información:  

- **Acción**: en la lista desplegable, seleccione si la implementación va a **Instalar** o **Desinstalar** la aplicación.  

    > [!NOTE]  
    >  Si crea una implementación para **Instalar** una aplicación y otra implementación para **Desinstalar** la misma aplicación en el mismo dispositivo, tendrá prioridad la implementación para **Instalar**.  

    Después de crear la acción de una implementación, no se puede cambiar.  

- **Propósito**: en la lista desplegable, elija una de las opciones que se indican a continuación.  

    - **Disponible**: el usuario ve la aplicación en el Centro de software. Puede instalarla a petición.  

    - **Obligatoria**: el cliente instala automáticamente la aplicación según la programación que establezca. Si la aplicación no está oculta, un usuario puede realizar el seguimiento de su estado de implementación. También puede usar el Centro de software para instalar la aplicación antes de la fecha límite.  

    > [!NOTE]   
    >  Al establecer la acción de implementación en **Desinstalar**, el propósito de implementación se establecerá automáticamente en **Obligatoria**. Este comportamiento no se puede cambiar.  

- **Implementar previamente el software en el dispositivo primario del usuario**: si la implementación se realiza en un usuario, seleccione esta opción para implementar la aplicación en el dispositivo principal del usuario. Esta opción no exige que el usuario inicie sesión antes de que se ejecute la implementación. Si el usuario necesita interactuar con la instalación, no seleccione esta opción. Esta opción solo está disponible cuando la implementación es **Obligatoria**.  

- **Enviar paquetes de reactivación**: si la implementación es **Obligatoria**, Configuration Manager envía un paquete de reactivación a los equipos antes de que el cliente ejecute la implementación. Este paquete reactiva el equipo a la hora límite de instalación. Para poder usar esta opción, los equipos y las redes deben configurarse para Wake On LAN. Para obtener más información, vea [Planear la reactivación de clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

- **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales**: esta opción solo está disponible para implementaciones con un propósito **Requerido**.  

- **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**: el cliente actualiza cualquier versión reemplazada de la aplicación con la aplicación nueva. 

    > [!Note]  
    > Esta opción siempre funciona, independientemente de la aprobación del administrador. Si un administrador ya aprobó la versión reemplazada, no necesitará aprobar también la versión que sustituye. La aprobación solo es necesaria para nuevas solicitudes, no para actualizaciones que sustituyen.<!--515824-->  

    > [!NOTE]  
    > A partir de la versión 1802, esta opción se puede habilitar o deshabilitar para el propósito de instalación **Disponible**. <!--1351266--> 


#### <a name="bkmk_approval"></a> Configuración de aprobación
Se mostrará una de las siguientes opciones de configuración de aprobación, según su versión de Configuration Manager:

- **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación**: para las versiones 1710 y anteriores, el administrador aprueba las solicitudes de la aplicación de cualquier usuario antes de poder instalarla. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos.  

    Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aprobación** , en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** . Si una solicitud no se aprueba antes de 45 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

    Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  

- **An administrator must approve a request for this application on the device** (Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo): a partir de la versión 1802, el administrador aprueba las solicitudes de usuario para la aplicación antes de que el usuario pueda instalarla en el dispositivo solicitado. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. La opción está atenuada cuando el propósito de implementación es **Obligatorio**, o bien cuando se implementa la aplicación en una colección de dispositivos. <!--1357015-->  

    Esta característica es opcional. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Si no habilita esta característica, verá la experiencia anterior.  

    > [!Note]  
    > Para aprovechar las nuevas características de Configuration Manager, primero actualice los clientes a la versión más reciente. Aunque la funcionalidad nueva aparece en la consola de Configuration Manager cuando se actualiza el sitio y la consola, la totalidad del escenario no es funcional hasta que la versión del cliente también es la más reciente.<!--SCCMDocs issue 646-->  

    Vea **Solicitudes de aprobación** en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** de la consola de Configuration Manager. Hay una columna **Dispositivo** en la lista de cada solicitud. Al realizar acciones en la solicitud, el cuadro de diálogo Solicitud de aplicación también incluye el nombre del dispositivo desde el que el usuario envió la solicitud.  

    Si una solicitud no se aprueba antes de 45 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  

    Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos. Impide que los usuarios instalen nuevas copias de la aplicación desde el Centro de software.  

    > [!Important]  
    > A partir de la versión 1806, *el comportamiento ha cambiado* al revocar la aprobación de una aplicación que se haya aprobado e instalado anteriormente. Ahora, al **Denegar** la solicitud de la aplicación, el cliente desinstala la aplicación del dispositivo del usuario.<!--1357891-->  


#### <a name="deployment-properties-deployment-settings"></a>Configuración de **propiedades de implementación**
Al ver las propiedades de una implementación, si la tecnología del tipo de implementación lo admite, se mostrará la siguiente opción en la pestaña **Configuración de implementación**:

**Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**. Para obtener más información, vea [Comprobar archivos ejecutables en ejecución antes de instalar una aplicación](#bkmk_exe-check).



### <a name="bkmk_deploy-sched"></a> Configuración de la **programación** de implementaciones

En la página **Programación**, establezca la hora en que se implementará esta aplicación o estará disponible para los dispositivos cliente.

De forma predeterminada, Configuration Manager hace que la directiva de implementación esté disponible para los clientes de forma inmediata. Si quiere crear la implementación, pero no quiere que esté disponible para los clientes hasta una fecha posterior, establezca la opción en **Programar la aplicación para que esté disponible**. Después, seleccione la fecha y hora, y especifique si se basan en UTC o en la hora local del cliente. 

Si la implementación es **Obligatoria**, especifique también la **Fecha límite de instalación**. De forma predeterminada, esta fecha límite es lo antes posible. 

Por ejemplo, necesita implementar una nueva aplicación de línea de negocio. Todos los usuarios necesitan instalarla antes de un momento específico, pero quiere proporcionarles la opción de instalarla de forma opcional anteriormente. Además, necesita asegurarse de que el sitio distribuya el contenido a todos los puntos de distribución. Programe la aplicación para que esté disponible en un plazo de cinco días desde el día actual. Esta programación le proporciona tiempo para distribuir el contenido y confirmar su estado. Después, establezca la fecha límite de instalación en un mes a partir del día actual. Los usuarios verán la aplicación en el Centro de software cuando esté disponible en un plazo de cinco días. Si no realiza ninguna acción, el cliente instalará automáticamente la aplicación en la fecha límite de instalación. 

Si la aplicación que quiere implementar sustituye a otra aplicación, establezca la fecha límite de instalación cuando los usuarios reciban la nueva aplicación. Establezca la **Fecha límite de instalación** para actualizar los usuarios con la aplicación sustituida.


#### <a name="delay-enforcement-with-a-grace-period"></a>Retrasar el cumplimiento con un período de gracia
Puede que quiera ofrecer más tiempo a los usuarios para instalar las aplicaciones obligatorias *más allá* de las fechas límite que establezca. Este comportamiento suele ser necesario cuando un equipo está desactivado durante un tiempo prolongado y es necesario instalar un gran número de aplicaciones. Por ejemplo, cuando un usuario vuelve de vacaciones, tiene que esperar mucho tiempo mientras el cliente instala las implementaciones atrasadas. Para solucionar este problema, defina un período de gracia de cumplimiento.

- Primero, configure este período de gracia con la propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** en la configuración del cliente. Para obtener más información, vea el grupo [Agente de equipo](/sccm/core/clients/deploy/about-client-settings#computer-agent). Especifique un valor entre **1** y **120** horas.  

- En la página **Programación** de una implementación de aplicación obligatoria, habilite la opción **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**. El período de gracia de cumplimiento se aplica a todas las implementaciones que tienen habilitada esta opción y que están destinadas a dispositivos en los que también se ha implementado la configuración del cliente.

Después de la fecha límite, el cliente instalará la aplicación en la primera ventana fuera del horario laboral que haya configurado el usuario, hasta ese período de gracia. Pero el usuario aún podrá abrir el Centro de software e instalar la aplicación en cualquier momento. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.


### <a name="bkmk_deploy-ux"></a> Configuración de la **experiencia del usuario** de implementación

En la página **Experiencia del usuario**, especifique información sobre cómo los usuarios pueden interactuar con la instalación de aplicaciones.

- **Notificaciones de usuario**: especifique si se muestran notificaciones en el Centro de software en la hora disponible configurada. Esta opción también controla si se notifica a los usuarios en los equipos cliente. Para las implementaciones disponibles, no se puede seleccionar la opción **Ocultar en el Centro de software y ocultar todas las notificaciones**.  

- **Instalación de software** y **Reinicio del sistema**: solo configure estas opciones para las implementaciones necesarias. Estas opciones especifican los comportamientos cuando la implementación alcanza la fecha límite más allá de las ventanas de mantenimiento definidas. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](/sccm/core/clients/manage/collections/use-maintenance-windows).  

- **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta configuración controla el comportamiento de instalación en dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. De lo contrario, la aplicación se instala en la superposición temporal y se confirma más tarde.  

    - Al implementar una actualización de software en un dispositivo de Windows Embedded, asegúrese de que el dispositivo sea miembro de una colección que tenga configurada una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento y los dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications).  


### <a name="bkmk_deploy-alerts"></a> Alertas de **implementación**

En la página **Alertas**, configure la forma en que Configuration Manager genera las alertas para esta implementación. Si también usa System Center Operations Manager, configure también sus alertas. Solo se pueden configurar algunas alertas para las implementaciones necesarias. 


### <a name="bkmk_deploy-ios"></a> iOS: **Directivas de configuración de aplicaciones**

Al implementar un tipo de implementación de iOS, también verá la página **Directivas de configuración de aplicaciones**. Si ya ha creado una directiva de configuración de aplicaciones de iOS, haga clic en **Nuevo** para asociar esta implementación con la directiva. Para obtener más información sobre este tipo de directiva, consulte [Configure iOS apps with app configuration policies](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurar aplicaciones iOS con directivas de configuración de aplicaciones).



## <a name="bkmk_phased"></a> Creación de una implementación por fases
<!--1358147--> A partir de la versión 1806, se puede crear una implementación por fases para una aplicación. Las Implementaciones por fases permiten organizar un lanzamiento de software coordinado y secuencial según criterios y grupos personalizables. Por ejemplo, implemente la aplicación en una colección piloto y luego continúe automáticamente con la implementación según los criterios de éxito. 

Vea los siguientes artículos para más información:  

- [Creación de una implementación por fases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Administración y supervisión de implementaciones por fases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="bkmk_delete"></a> Eliminar una implementación

1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones** y seleccione el nodo **Aplicaciones**.  

2.  En la lista **Aplicaciones**, seleccione la aplicación que contenga la implementación que quiera eliminar.  

3.  Cambie a la pestaña **Implementaciones** del panel de detalles y seleccione la implementación de aplicaciones.  

4. En la cinta de opciones, en el grupo **Implementación** de la pestaña **Implementación**, haga clic en **Eliminar**.  

Al eliminar una implementación de aplicaciones, no se desinstalarán las instancias de la aplicación que los clientes ya hayan instalado. Para desinstalar estas aplicaciones, implemente la aplicación en los equipos con la opción **Desinstalar**. Si elimina una implementación de aplicaciones o quita un recurso de la colección donde realice la implementación, la aplicación ya no será visible en el Centro de software.



## <a name="bkmk_notify"></a> Notificaciones de usuario para implementaciones obligatorias

Cuando los usuarios reciben software obligatorio y seleccionan la opción **Posponer y volver a recordármelo**, pueden seleccionar entre las opciones siguientes:  

- **Más adelante**: especifica que las notificaciones se programan según la configuración de notificación establecida en la configuración del cliente.  

- **Hora fija**: especifica que la notificación se programa para mostrarse de nuevo después de la hora seleccionada. Por ejemplo, si selecciona 30 minutos, la notificación se mostrará de nuevo transcurrido ese tiempo.  

![Grupo Agente de equipo en la configuración de cliente predeterminada](media/ComputerAgentSettings.png)

El tiempo de aplazamiento máximo siempre se basa en los valores de notificación establecidos en la configuración del cliente en cada momento a lo largo de la escala de tiempo de implementación. Por ejemplo:  

- El valor **La fecha límite de la implementación es de más de 24 horas. Recordar al usuario cada (horas)** se configura en la página **Agente de equipo** para 10 horas.  

- El cliente muestra el cuadro de diálogo de notificación más de 24 horas antes de la fecha límite de la implementación.  

- En el cuadro de diálogo se muestran las opciones de aplazamiento hasta 10 horas, pero nunca más.   

- Cuando se acerca la fecha límite de la implementación, en el cuadro de diálogo se muestran menos opciones. Estas opciones son coherentes con la configuración de cliente relevante para cada componente de la escala de tiempo de implementación.  

En una implementación de alto riesgo, como una secuencia de tareas que implementa un sistema operativo, la experiencia de notificación del usuario es más intrusiva. En lugar de una notificación transitoria en la barra de tareas, en un cuadro de diálogo como el siguiente se muestra cada vez que se le notifica que se necesita mantenimiento de software crítico:

![Cuadro de diálogo Software requerido en el que se notifica el mantenimiento de software crítico](media/client-toast-notification.png)



## <a name="bkmk_exe-check"></a> Comprobar archivos ejecutables en ejecución

Configure una implementación para comprobar si determinados archivos ejecutables se están ejecutando en el cliente. Use esta opción para comprobar los procesos que podrían interrumpir la instalación de la aplicación. Si uno de estos archivos ejecutables está ejecutándose, el cliente impedirá la instalación del tipo de implementación. El usuario debe cerrar el archivo ejecutable en ejecución antes de que el cliente pueda instalar el tipo de implementación. Para las implementaciones con un propósito de Requerido, el cliente puede cerrar automáticamente el archivo ejecutable en ejecución.

1. Abra el cuadro de diálogo **Propiedades** del tipo de implementación.  

2. Vaya a la pestaña **Comportamiento de instalación** y haga clic en **Agregar**.  

3. En el cuadro de diálogo **Agregar archivo ejecutable**, escriba el nombre del archivo ejecutable de destino. De manera opcional, escriba un nombre descriptivo para la aplicación que le ayude a identificarla en la lista.  

4. Haga clic en **Aceptar** y, después, seleccione **Aceptar** para cerrar la ventana de propiedades del tipo de implementación.  

5. Al implementar la aplicación, seleccione la opción **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**. Esta opción se encuentra en la pestaña **Configuración de implementación** de las propiedades de la implementación.  


### <a name="client-behaviors-and-user-notifications"></a>Comportamientos de cliente y notificaciones de usuario

Después de que los clientes reciban la implementación, se aplica el comportamiento siguiente:  

- Si ha implementado la aplicación como **Disponible** y un usuario intenta instalarla, el cliente le pedirá al usuario que cierre los archivos ejecutables especificados que estén ejecutándose antes de continuar con la instalación.  

- Si ha implementado la aplicación como **Obligatoria** y ha especificado la opción **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, se mostrará una notificación en el cliente. Informará al usuario de que los archivos ejecutables especificados se cerrarán automáticamente cuando se alcance la fecha límite de instalación de la aplicación.  

    - Programe estos cuadros de diálogo en el grupo **Agente de equipo** de la configuración del cliente. Para obtener más información, vea [Agente de equipo](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    - Si no quiere que el usuario vea estos mensajes, seleccione la opción **Ocultar en el Centro de software y ocultar todas las notificaciones** en la pestaña **Experiencia del usuario** de las propiedades de la implementación. Para obtener más información, vea [Configuración de la experiencia del usuario de implementación](#bkmk_deploy-ux).  

- Si la aplicación se implementó como **Requerido** y no se especificó **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, se produce un error en la instalación de la aplicación si una o varias de las aplicaciones especificadas está en ejecución.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implementar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD
<!-- 1322613 --> Si se implementan aplicaciones como disponibles para los usuarios, a partir de la versión 1802 pueden examinarlas e instalarlas a través del Centro de software en dispositivos de Azure Active Directory (Azure AD).  

#### <a name="prerequisites"></a>Requisitos previos

- Habilitar el HTTPS en el punto de administración  

- Integrar el sitio con [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) para **administración en la nube**  

    - Configurar la [detección de usuarios de Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Implementar una aplicación como disponible para una colección de usuarios desde Azure AD  

- Distribuir el contenido de la aplicación a un [punto de distribución en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Habilitar la configuración de cliente **Usar nuevo Centro de software** en el grupo [Agente de equipo](/sccm/core/clients/deploy/about-client-settings#computer-agent)  

- El sistema operativo de cliente debe ser Windows 10 y estar unido a Azure AD. Puede estar unido a un dominio en la nube pura o a Azure AD híbrido.  

- Para admitir clientes basados en Internet:  

    - [Puerta de enlace de administración en la nube](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Habilitar la configuración de cliente **Habilitar solicitudes de directiva de usuario de clientes de Internet** en el grupo [Directiva de cliente](/sccm/core/clients/deploy/about-client-settings#client-policy)  

- Para admitir clientes en la intranet:  

    - Agregar el punto de distribución en la nube a un grupo de límites utilizado por los clientes  

    - Los clientes necesitan resolver el nombre de dominio completo (FQDN) del punto de administración habilitado para HTTPS.  



## <a name="next-steps"></a>Pasos siguientes
 - [Supervisar aplicaciones](/sccm/apps/deploy-use/monitor-applications-from-the-console)
 - [Tareas de administración para aplicaciones](/sccm/apps/deploy-use/management-tasks-applications)
 - [Manual del usuario del Centro de software](/sccm/core/understand/software-center)

