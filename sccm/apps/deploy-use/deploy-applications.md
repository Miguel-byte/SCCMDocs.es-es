---
title: Implementar aplicaciones
titleSuffix: Configuration Manager
description: Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a89c9d5a0fa4ea57a7824fe16b24120347ddaac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338040"
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Implementar aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Crear o simular una implementación de una aplicación en una recopilación de dispositivo o usuario en Configuration Manager. Esta implementación proporciona instrucciones para el cliente de Configuration Manager sobre cómo y cuándo instalar el software. 

Antes de implementar una aplicación, cree al menos un tipo de implementación para la aplicación. Para obtener más información, consulte [Create applications](/sccm/apps/deploy-use/create-applications) (Creación de aplicaciones).

 También puede simular la implementación de una aplicación. Esta simulación prueba la aplicabilidad de una implementación sin instalar o desinstalar la aplicación. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión**. Para obtener más información, consulte el artículo sobre [simular implementaciones de aplicaciones ](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Puede simular la implementación de aplicaciones necesarias, pero no de paquetes o actualizaciones de software.   
>  Los dispositivos inscritos en MDM no admiten las implementaciones simuladas, la experiencia del usuario o la configuración de programación.



## <a name="deploy-an-application"></a>Implementar una aplicación

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.

2.  En la lista de **Aplicaciones** , seleccione la aplicación que desee implementar. A continuación, en la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Implementar**.

### <a name="specify-general-information-about-the-deployment"></a>Especificar información general sobre la implementación

En la página **General** del Asistente para implementar software, especifique la información siguiente:

- **Software**: este valor muestra la aplicación que se va a implementar. Haga clic en **Examinar** para seleccionar otra aplicación.
- **Recopilación**: haga clic en **Examinar** para seleccionar la recopilación en la que se va a implementar la aplicación.
- **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: almacene el contenido de la aplicación en el grupo de puntos de distribución predeterminado de la recopilación. Si no asocia la recopilación seleccionada con un grupo de puntos de distribución, esta opción aparecerá atenuada.
- **Distribuir contenido automáticamente para las dependencias**: si cualquiera de los tipos de implementación de la aplicación contiene dependencias, el sitio también envía contenido de la aplicación dependiente a los puntos de distribución.

    >[!IMPORTANT]
    > Si actualiza la aplicación dependiente después de implementar la aplicación principal, el sitio no distribuye automáticamente ningún contenido nuevo para la dependencia.

- **Comentarios (opcional)**: si quiere, escriba una descripción para esta implementación.

### <a name="specify-content-options-for-the-deployment"></a>Especificar las opciones de contenido de la implementación

En la página **Contenido**, haga clic en **Agregar** para agregar el contenido asociado a esta implementación a los puntos de distribución o grupos de puntos de distribución. Si selecciona **Usar puntos de distribución predeterminados asociados a esta recopilación** en la página **General**, esta opción se rellena automáticamente. Solo un miembro del rol de seguridad Administrador de la aplicación puede modificarla.

### <a name="specify-deployment-settings"></a>Especificar la configuración de implementación

En la página **Configuración de implementación** del Asistente para implementar software, especifique la información siguiente:

- **Acción**: en la lista desplegable, seleccione si la implementación va a **Instalar** o **Desinstalar** la aplicación.

    > [!NOTE]
    >  Si una aplicación se implementa dos veces en un dispositivo, una vez con una acción de **Instalar** y otra con una acción de **Desinstalar**, la implementación de la aplicación con una acción de **Instalar** tendrá prioridad.

  No se puede cambiar la acción de una implementación después de crearla.

- **Propósito**: en la lista desplegable, elija una de las opciones que se indican a continuación.  
    - **Disponible**: si la aplicación se implementa en un usuario, este la ve publicada en el Centro de software y la puede instalar a petición.
    - **Requerido**: la aplicación se implementa automáticamente según la programación. Si el estado de implementación de la aplicación no está oculto, cualquier persona que use la aplicación puede realizar un seguimiento de su estado de implementación e instalar la aplicación desde el Centro de software antes de la fecha límite.

    > [!NOTE]   
    >  Cuando la acción de implementación se establece en **Desinstalar**, el propósito de la implementación se establece automáticamente en **Requerido**. Este comportamiento no se puede cambiar.  

- **Implementar automáticamente según la programación tanto si un usuario inició sesión como si no**: si la implementación es en un usuario, seleccione esta opción para implementar la aplicación en los dispositivos primarios del usuario. Esta configuración no requiere que el usuario inicie sesión para ejecutar la implementación. No seleccione esta opción si el usuario debe interactuar con la instalación. Esta opción solo está disponible cuando la implementación tiene un propósito **Requerido**.

- **Enviar paquetes de reactivación**: si el propósito de la implementación se establece en **Requerido**, se envía un paquete de reactivación a los equipos antes de que el cliente ejecute la implementación. Este paquete reactiva el equipo a la hora límite de instalación. Para poder usar esta opción, los equipos y las redes deben configurarse para Wake On LAN.
- **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales**: esta opción solo está disponible para implementaciones con un propósito **Requerido**.
- **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**: para obtener más información, vea [Comprobación de los archivos ejecutables en ejecución antes de instalar una aplicación](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Solicitar aprobación del administrador si los usuarios solicitan esta aplicación**: para las versiones 1710 y anteriores, el administrador aprueba las solicitudes de la aplicación de cualquier usuario antes de poder instalarla. Esta opción aparece atenuada si el propósito de la implementación es **Requerido** o si se implementa la aplicación en una recopilación de dispositivos.  

    > [!NOTE]
    >  Las solicitudes de aprobación de aplicación se muestran en el nodo **Solicitudes de aprobación** , en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** . Si una solicitud no se aprueba antes de 45 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  
    >  Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos, pero impide que los usuarios instalen copias nuevas de la aplicación desde el Centro de software.

- **An administrator must approve a request for this application on the device** (Un administrador debe aprobar una solicitud para esta aplicación en el dispositivo): a partir de la versión 1802, el administrador aprueba las solicitudes de usuario para la aplicación antes de que el usuario pueda instalarla en el dispositivo solicitado. Si el administrador aprueba la solicitud, el usuario solo tiene la posibilidad de instalar la aplicación en ese dispositivo. El usuario debe enviar otra solicitud para instalar la aplicación en otro dispositivo. Esta opción aparece atenuada si el propósito de la implementación es **Requerido** o si se implementa la aplicación en una recopilación de dispositivos. <!--1357015-->  

    Esta característica es opcional. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Si esta característica no está habilitada, verá la experiencia anterior.  

    > [!Important]  
    > La versión del cliente de Configuration Manager también debe ser la 1802. También debe usar el nuevo Centro de software.  

    > [!Note]  
    > Vea **Solicitudes de aprobación** en **Administración de aplicaciones** en el área de trabajo **Biblioteca de software** de la consola de Configuration Manager. Ahora hay una columna **Dispositivo** en la lista para cada solicitud. Al realizar acciones en la solicitud, el cuadro de diálogo Solicitud de aplicación también incluye el nombre del dispositivo desde el que el usuario envió la solicitud.  
    >  Si una solicitud no se aprueba antes de 45 días, se quita. Es posible que volver a instalar el cliente cancele las solicitudes de aprobación pendientes.  
    >  Después de aprobar una aplicación para la instalación, puede **Denegar** la solicitud en la consola de Configuration Manager. Esta acción no hace que el cliente desinstale la aplicación de los dispositivos, pero impide que los usuarios instalen copias nuevas de la aplicación desde el Centro de software.

- **Actualizar automáticamente cualquier versión reemplazada de esta aplicación**: el cliente actualiza cualquier versión reemplazada de la aplicación con la aplicación nueva.    

    > [!NOTE]  
    > A partir de la versión 1802, esta opción se puede habilitar o deshabilitar para el propósito de instalación **Disponible** o **Requerido**. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Especificar la configuración de programación de la implementación

En la página **Programación** del Asistente para implementar software, establezca cuándo se implementará o estará disponible para dispositivos cliente esta aplicación.
Las opciones de esta página variarán dependiendo de si la acción de la implementación se establece en **Disponible** o **Requerido**.

En algunos casos, es posible que quiera dar más tiempo a los usuarios para instalar las implementaciones de aplicaciones o las actualizaciones de software necesarias más allá de los plazos que ha establecido. Este comportamiento es normalmente necesario cuando un equipo ha estado apagado durante mucho tiempo y necesita instalar muchas aplicaciones. Por ejemplo, si un usuario final ha vuelto de vacaciones, es posible que tenga que esperar bastante mientras se instalan las implementaciones de aplicaciones vencidas. Para solucionar este problema, puede definir un período de gracia de cumplimiento mediante la implementación de la configuración de cliente de Configuration Manager en una colección.

Para configurar el período de gracia, haga lo siguiente:

- En la página **Agente de equipo** de la configuración de cliente, configure la nueva propiedad **Período de gracia para el cumplimiento tras la fecha límite de la implementación (horas)** con un valor entre **1** y **120** horas.
- En la página **Programación** de una implementación de aplicación requerida, seleccione **Retrasar el cumplimiento de esta implementación de acuerdo con las preferencias del usuario hasta el período de gracia definido en la configuración del cliente**. El período de gracia de cumplimiento se aplica a todas las implementaciones que tienen habilitada esta opción y que están destinadas a dispositivos en los que también se ha implementado la configuración del cliente.

Una vez que se alcance la fecha límite de instalación de la aplicación, el cliente la instala en la primera ventana que no sea de empresa, configurada por el usuario, hasta ese período de gracia. No obstante, el usuario puede abrir el Centro de software e instalar la aplicación en cualquier momento que quiera. Una vez que expira el período de gracia, el cumplimiento vuelve al comportamiento normal para implementaciones vencidas.

Si la aplicación que se va a implementar reemplaza a otra, se puede establecer la fecha límite de instalación cuando los usuarios reciban la aplicación nueva. Establezca la **Fecha límite de instalación** para actualizar los usuarios con la aplicación sustituida.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Especificar la configuración de la experiencia del usuario para la implementación

En la página **Experiencia del usuario** del Asistente para implementar software, especifique información sobre cómo pueden interactuar los usuarios con la instalación de la aplicación.

Cuando se implementan aplicaciones en dispositivos de Windows Embedded habilitados para filtro de escritura, se puede especificar que se instale la aplicación en la superposición temporal y confirmar los cambios más tarde. También se puede especificar que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Si los cambios se confirman en la fecha límite de instalación o durante una ventana de mantenimiento, es necesario reiniciar el dispositivo. Los cambios se conservan en el dispositivo.

>[!NOTE]
    >  Cuando se implementa una aplicación en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación con una ventana de mantenimiento. Para obtener más información sobre las ventanas de mantenimiento y los dispositivos de Windows Embedded, vea [Creación de aplicaciones de Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > Las opciones **Instalación de software** y **Reinicio del sistema (si es necesario para completar la instalación)** no se usan si el propósito de la implementación está establecido en **Disponible**. También puede configurar el nivel de notificación que ve un usuario cuando se instala la aplicación.

### <a name="specify-alert-options-for-the-deployment"></a>Especificar las opciones de alerta de la implementación

En la página **Alertas** del Asistente para implementar software, establezca cómo Configuration Manager y System Center Operations Manager generarán alertas para esta implementación. Puede configurar umbrales para alertas de generación de informes y desactivar los informes durante la implementación.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Asociar la implementación con una directiva de configuración de aplicaciones iOS

En la página **Directivas de configuración de aplicaciones**, haga clic en **Nuevo** para asociar esta implementación con una directiva de configuración de aplicaciones iOS (si ha creado una). Para obtener más información sobre este tipo de directiva, consulte [Configure iOS apps with app configuration policies](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurar aplicaciones iOS con directivas de configuración de aplicaciones).

### <a name="deployment-properties"></a>Propiedades de implementación

Busque la implementación nueva en el nodo **Implementaciones** del área de trabajo **Supervisión**. Puede editar las propiedades de esta implementación o eliminar la implementación de la pestaña **Implementaciones** del panel de detalles de la aplicación.



## <a name="delete-an-application-deployment"></a>Eliminar la implementación de una aplicación

1.  En la consola de Configuration Manager, vaya a **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.
3.  En la lista **Aplicaciones**, seleccione la aplicación que incluya la implementación que se va a eliminar.
4.  En la pestaña **Implementaciones** de la lista *<nombre de aplicación\>*, seleccione la implementación de la aplicación que desee eliminar. Después, en la pestaña **Implementación**, en el grupo **Implementación**, haga clic en **Eliminar**.

Cuando se elimina una implementación de aplicación, no se quitan las instancias de la aplicación que ya se han instalado. Para quitar estas aplicaciones, debe implementar la aplicación en los equipos con la opción **Desinstalar**. Si se elimina una implementación de aplicación o se quita un recurso de la recopilación en la que se está implementando, la aplicación ya no será visible en el Centro de software.



## <a name="user-notifications-for-required-deployments"></a>Notificaciones de usuario para las implementaciones requeridas
Cuando recibe software obligatorio a través de la opción **Snooze and remind me** (Posponer y volver a recordármelo), puede seleccionar los siguientes valores en la lista desplegable:
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



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Comprobación de los archivos ejecutables en ejecución antes de instalar una aplicación

En el cuadro de diálogo **Propiedades** de un tipo de implementación, en la pestaña **Comportamiento de instalación**, especifique uno o más archivos ejecutables. Si uno de estos archivos ejecutables se ejecuta en el cliente, se bloquea la instalación del tipo de implementación. El usuario debe cerrar el archivo ejecutable en ejecución antes de que el cliente pueda instalar el tipo de implementación. Para las implementaciones con un propósito de Requerido, el cliente puede cerrar automáticamente el archivo ejecutable en ejecución.

1. Abra el cuadro de diálogo **Propiedades** para cualquier tipo de implementación.
2. En la pestaña **Comportamiento de instalación** del cuadro de diálogo *<deployment type name>* **Propiedades** y haga clic en **Agregar**.
3. En el cuadro de diálogo **Agregar o editar archivo ejecutable**, escriba el nombre del archivo ejecutable que, si se ejecuta, bloqueará la instalación de la aplicación. Si lo desea, también puede escribir un nombre descriptivo para la aplicación, a fin de facilitar su identificación en la lista.
4. Haga clic en **Aceptar** y luego cierre el cuadro de diálogo *<deployment type name>* **Propiedades**.
5. Al implementar la aplicación, en la página **Configuración de implementación** del Asistente para implementar software, seleccione **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**.

Después de que los clientes reciban la implementación, se aplica el comportamiento siguiente:

- Si la aplicación se implementó como **Disponible** y un usuario final trata de instalarla, el cliente solicita al usuario que cierre los archivos ejecutables en ejecución especificados antes de continuar con la instalación.

- Si la aplicación se implementó como **Requerido** y se especificó **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, el usuario verá un cuadro de diálogo que le informa de que los archivos ejecutables especificados se cerrarán automáticamente cuando se alcance la fecha límite de la instalación de la aplicación. Puede programar estos cuadros de diálogo en **Configuración de cliente** > **Agente de equipo**. Si no quiere que el usuario final vea estos mensajes, seleccione **Ocultar en el Centro de software y ocultar todas las notificaciones** en la pestaña **Experiencia del usuario** de las propiedades de la implementación.

- Si la aplicación se implementó como **Requerido** y no se especificó **Cerrar automáticamente los archivos ejecutables especificados en la ficha Comportamiento de instalación del cuadro de diálogo de propiedades Tipo de implementación que estén en ejecución**, se produce un error en la instalación de la aplicación si una o varias de las aplicaciones especificadas está en ejecución.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Implementar aplicaciones disponibles para el usuario en dispositivos unidos a Azure AD
<!-- 1322613 -->
Si se implementan aplicaciones como disponibles para los usuarios, a partir de la versión 1802 pueden examinarlas e instalarlas a través del Centro de software en dispositivos de Azure Active Directory (Azure AD).  

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

    - Los clientes deben poder resolver el nombre de dominio completo (FQDN) del punto de administración habilitado para HTTPS  



## <a name="next-steps"></a>Pasos siguientes

   -  [Settings to manage high-risk deployments (Configuración para administrar implementaciones de alto riesgo)](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Cómo establecer la configuración del cliente](../../core/clients/deploy/configure-client-settings.md)
   -  [Manual del usuario del Centro de software](/sccm/core/understand/software-center)

