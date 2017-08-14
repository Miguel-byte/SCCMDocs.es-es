---
title: "Configurar la detección | Microsoft Docs"
description: "Configure métodos de detección para que se ejecuten en un sitio de Configuration Manager a fin de detectar recursos que se puedan administrar desde la infraestructura de red y Active Directory."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 0663ba84762c44a5c303562548499f195bae9e1c
ms.openlocfilehash: 34a539ceaea6b070f81a28d2c0a9ce388e26cfeb
ms.contentlocale: es-es
ms.lasthandoff: 08/01/2017

---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurar métodos de detección para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*


Puede configurar métodos de detección que se ejecuten en un sitio de System Center Configuration Manager a fin de detectar recursos que se puedan administrar desde la infraestructura de red y Active Directory. Esto exige habilitar y luego configurar cada método que quiera usar para realizar búsquedas en el entorno. (También se puede deshabilitar un método con el mismo procedimiento que se use para habilitarlo).  Las únicas excepciones a esto son la detección de latidos y la detección de servidores:  

-   De forma predeterminada, la detección de latidos ya está habilitada al instalar un sitio primario de Configuration Manager y configurada para ejecutarse en una programación básica. Es conveniente mantener habilitada la detección de latidos, porque garantiza que los registros de datos de detección (DDR) de los dispositivos estén actualizados. Para obtener más información sobre la detección de latidos, vea [Acerca de la detección de latidos](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   La detección de servidores es un método de detección automático que busca equipos que se usen como sistemas de sitio. No se puede configurar ni deshabilitar.  

**Para habilitar un método de detección configurable, siga estos pasos:**  
 > [!NOTE]  
 > La siguiente información no se aplica a la funcionalidad de detección de usuarios de Azure Active Directory. En su lugar, consulte la sección [configurar usuarios de Azure AD detección](#azureaadisc) más adelante en este tema.

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Seleccione el método de detección para el sitio donde desea habilitar la detección.  

3.  En el grupo **Propiedades** de la pestaña **Inicio**, elija **Propiedades** y luego, en la pestaña **General**, active la casilla **Habilitar&lt;método de detección\>**.  

     Si esta casilla ya está activada, puede desactivarla para deshabilitar el método de detección.  

4.  Elija **Aceptar** para guardar la configuración.  


##  <a name="BKMK_ConfigADForestDisc"></a> Configuración de la detección de bosques de Active Directory  
Para finalizar la configuración de detección de bosques de Active Directory, debe realizar configuraciones en dos ubicaciones:  

-   En el nodo **Métodos de detección**, puede:

    - Habilitar este método de detección.
    - Establecer una programación de sondeo.
    - Seleccione si la detección crea automáticamente límites para los sitios y subredes de Active Directory que detecta.  

-   En el nodo **Bosques de Active Directory**, puede:

    - Agregar bosques que quiere detectar.
    - Habilitar la detección sitios y subredes de Active Directory en el bosque.
    - Configurar opciones que habiliten sitios de Configuration Manager para publicar la información del sitio en el bosque.
    - Asignar una cuenta para utilizarla como la cuenta de bosque de Active Directory de cada bosque.  

Utilice los procedimientos siguientes para habilitar la detección de bosques de Active Directory y configurar bosques individuales a fin de utilizarlos con la detección de bosques de Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Para habilitar la detección de bosques de Active Directory  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Seleccione el método Detección de bosques de Active Directory para el sitio donde desea configurar la detección.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En la pestaña **General**, active la casilla para habilitar la detección. También puede configurar ahora la detección y volver después para habilitarla.  

5.  Especifique opciones para crear los límites de sitio para las ubicaciones detectadas.  

6.  Especifique una programación de ejecución de la detección.  

7.  Cuando termine la configuración de la detección de bosques de Active Directory para este sitio, elija **Aceptar** para guardar la configuración.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Para configurar un bosque para la detección de bosques de Active Directory  

1.  En el área de trabajo **Administración**, elija **Bosques de Active Directory**. Si previamente ejecutó la detección de bosques de Active Directory, verá cada bosque detectado en el panel de resultados. El bosque local y todos los bosques de confianza se detectan cuando se ejecuta la detección de bosques de Active Directory. Sólo deben agregarse manualmente los bosques que no son de confianza.  

    -   Para configurar un bosque detectado anteriormente, seleccione el bosque en el panel de resultados. Después, en el grupo **Propiedades** de la pestaña **Inicio**, elija **Propiedades** para abrir las propiedades del bosque. Continúe con el paso 3.  

    -   Para configurar un nuevo bosque que no aparece en la lista, en el grupo **Crear** de la pestaña **Inicio**, elija **Agregar bosque** para abrir el cuadro de diálogo **Agregar bosques**. Continúe con el paso 3.  

2.  En la pestaña **General**, finalice las configuraciones del bosque que desea detectar y especifique la **cuenta de bosque de Active Directory**.  

    > [!NOTE]  
    >  La detección de bosques de Active Directory requiere una cuenta global para detectar bosques que no son de confianza y publicar en ellos. Si no utiliza la cuenta de equipo del servidor de sitio, solo se puede seleccionar una cuenta global.  

3.  Si piensa permitir que los sitios publiquen datos del sitio en este bosque, finalice las configuraciones necesarias para publicar en este bosque en la pestaña **Publicación**.  

    > [!NOTE]  
    >  Si permite que los sitios publiquen en un bosque, tendrá que extender el esquema de Active Directory del bosque para Configuration Manager. Es preciso que la cuenta de bosque de Active Directory tenga permisos de control total en el contenedor del sistema del bosque.  

4.  Cuando termine la configuración de este bosque para su uso con la detección de bosques de Active Directory, elija **Aceptar** para guardar la configuración.  

##  <a name="BKMK_ConfigADDiscGeneral"></a> Configuración de la detección de Active Directory para equipos, usuarios o grupos  
 Utilice la información de las secciones siguientes para configurar la detección de equipos, usuarios o grupos. Utilizará estos métodos de detección:  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

> [!NOTE]  
>  La información de esta sección no se aplica a la detección de bosques de Active Directory.  

 Si bien cada uno de estos métodos de detección es independiente del resto, comparten opciones similares. Para más información sobre estas opciones de configuración, vea [Shared options for Group, System, and User discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared) (Opciones compartidas para la detección de grupos, sistemas y usuarios).  

> [!WARNING]  
>  El sondeo de Active Directory de cada uno de estos métodos de detección puede generar un tráfico de red elevado. Puede programar los métodos de detección para que se ejecuten a la vez cuando este tráfico de red no afecte negativamente al uso que el negocio realiza de la red.  

#### <a name="to-configure-active-directory-group-discovery"></a>Para configurar la detección de grupos de Active Directory  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Elija el método **Detección de grupos de Active Directory** para el sitio donde desea configurar la detección.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En la pestaña **General**, active la casilla para habilitar la detección. También puede configurar ahora la detección y volver después para habilitarla.  

5.  Elija **Agregar** para configurar un ámbito de detección, elija **Grupos** o **Ubicación** y realice finalice las siguientes configuraciones en el cuadro de diálogo **Agregar grupos**o **Agregar ubicación de Active Directory**:  

    1.  Especifique un **Nombre** para este ámbito de detección.  

    2.  Especifique un **Dominio de Active Directory** o una **Ubicación** para buscar:  

        -   Si selecciona **Grupos**, especifique uno o varios grupos de Active Directory para su detección.  

        -   Si elige **Ubicación**, especifique un contenedor de Active Directory como ubicación que se deba detectar. También puede habilitar una búsqueda recursiva de los contenedores secundarios de Active Directory para esta ubicación.  

    3.  Especifique la **Cuenta de detección de grupos de Active Directory** utilizada para buscar este ámbito de detección.  

    4.  Elija **Aceptar** para guardar la configuración del ámbito de detección.  

6.  Repita el paso 6 para cada ámbito de detección adicional que desee definir.  

7.  En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.  

8.  De forma alternativa, en la pestaña **Opción**, puede configurar las opciones para filtrar o excluir de la detección los registros de equipos obsoletos, y para detectar la pertenencia a grupos de distribución.  

    > [!NOTE]  
    >  De forma predeterminada, la detección de grupos de Active Directory detecta únicamente la pertenencia a grupos de seguridad.  

9. Cuando haya terminado de configurar la detección de grupos de Active Directory para este sitio, elija **Aceptar** para guardar la configuración.  

#### <a name="to-configure-active-directory-system-discovery"></a>Para configurar la detección de sistemas de Active Directory  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Seleccione el método para el sitio donde desea configurar la detección.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En la pestaña **General**, active la casilla para habilitar la detección. También puede configurar ahora la detección y volver después para habilitarla.  

5.  Elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif) para especificar un nuevo contenedor de Active Directory. En el cuadro de diálogo **Contenedor de Active Directory**, finalice las configuraciones siguientes:  

    1.  Especifique una o varias ubicaciones de búsqueda.  

    2.  Para cada ubicación, especifique las opciones que modifican el comportamiento de búsqueda.  

    3.  Para cada ubicación, especifique la cuenta para utilizarla como la **Cuenta de detección de Active Directory**.  

        > [!TIP]  
        >  Para cada ubicación que especifique, puede configurar un conjunto de opciones de detección y una única cuenta de detección de Active Directory.  

    4.  Elija **Aceptar** para guardar la configuración del contenedor de Active Directory.  

6.  En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.  

7.  De forma alternativa, en la pestaña **Atributos de Active Directory** , puede configurar atributos adicionales de Active Directory para los equipos que desea detectar. También se enumeran los atributos predeterminados del objeto.  

8.  De forma alternativa, en la pestaña **Opción**, puede configurar las opciones para filtrar o excluir de la detección los registros de equipos obsoletos.  

9. Cuando haya terminado de configurar la detección de sistemas de Active Directory para este sitio, elija **Aceptar** para guardar la configuración.  

#### <a name="to-configure-active-directory-user-discovery"></a>Para configurar la detección de usuarios de Active Directory  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Elija el método **Detección de usuarios de Active Directory** para el sitio donde quiere configurar la detección.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  En la pestaña **General**, active la casilla para habilitar la detección. También puede configurar ahora la detección y volver después para habilitarla.  

5.  Elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif) para especificar un nuevo contenedor de Active Directory. En el cuadro de diálogo **Contenedor de Active Directory**, finalice las configuraciones siguientes:  

    1.  Especifique una o varias ubicaciones de búsqueda.  

    2.  Para cada ubicación, especifique las opciones que modifican el comportamiento de búsqueda.  

    3.  Para cada ubicación, especifique la cuenta para utilizarla como la **Cuenta de detección de Active Directory**.  

        > [!NOTE]  
        >  Para cada ubicación que especifique, puede configurar un conjunto único de opciones de detección y una única cuenta de detección de Active Directory.  

    4.  Elija **Aceptar** para guardar la configuración del contenedor de Active Directory.  

6.  En la pestaña **Programación de sondeo** , configure la programación de sondeo de detección completa y la detección de diferencias.  

7.  De forma alternativa, en la pestaña **Atributos de Active Directory** , puede configurar atributos adicionales de Active Directory para los equipos que desea detectar. También se enumeran los atributos predeterminados del objeto.  

8.  Cuando haya terminado de configurar la detección de usuarios de Active Directory para este sitio, elija **Aceptar** para guardar la configuración.  

## <a name="azureaadisc"></a>Configuración de la detección de usuarios de Azure AD
A partir de la versión 1706, puede configurar la detección de usuarios de Azure Active Directory cuando se conecta Configuration Manager a la [suscripción de Azure y a Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard).

La funcionalidad de detección de usuarios de Azure AD está configurada como parte de *Cloud Management Gateway*. El procedimiento se detalla en la sección [Creación de la aplicación web de Azure para utilizarla Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) del tema *Configuración de servicios de Azure para utilizarlos con Configuration Manager*.




##  <a name="BKMK_ConfigHBDisc"></a> Configuración de la detección de latidos  
 De forma predeterminada, la detección de latidos se habilita al instalar un sitio primario de Configuration Manager. Por consiguiente, solo tiene que configurar la programación de la frecuencia con que los clientes envían el registro de datos de detección de latidos a un punto de administración cuando no quiera usar el valor predeterminado de cada siete días.  

> [!NOTE]  
>  Si la instalación de inserción de cliente y la tarea de mantenimiento del sitio **Borrar marca de instalación** están habilitadas en el mismo sitio, establezca la programación de la detección de latidos para que sea inferior al **Periodo de nueva detección de cliente** de la tarea de mantenimiento del sitio **Borrar marca de instalación** . Para más información sobre las tareas de mantenimiento del sitio, vea [Maintenance tasks for System Center Configuration Manager (Tareas de mantenimiento para System Center Configuration Manager)](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Para configurar la programación de la detección de latidos  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Seleccione **Detección de latidos** para el sitio donde quiere configurar la detección de latidos.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  Configure la frecuencia con la que los clientes envían registros de datos de detección de latidos y luego elija **Aceptar** para guardar la configuración.  

##  <a name="BKMK_ConfigNetworkDisc"></a> Configuración de la detección de redes  
 Utilice la información de las secciones siguientes, que le facilitará la configuración de la detección de redes.  

###  <a name="BKMK_AboutConfigNetworkDisc"></a> Acerca de la configuración de la detección de redes  
 Antes de configurar la detección de redes, debe saber lo siguiente:  

-   Niveles disponibles de la detección de redes  

-   Opciones de detección de redes disponibles  

-   Limitar la detección de redes en la red  

Para obtener más información, vea la sección [Acerca de la detección de redes](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 En las secciones siguientes se proporciona información sobre configuraciones comunes para la detección de redes. Puede aplicar una o varias de estas configuraciones para utilizarlas durante la misma ejecución de la detección. Si utiliza varias configuraciones, debe planear las interacciones que pueden afectar a los resultados de la detección.  

 Por ejemplo, podría detectar todos los dispositivos de Protocolo Simple de administración de redes (SNMP) que utilicen un nombre de comunidad SNMP específico. Además, para la misma ejecución de la detección, puede deshabilitar la detección en una subred específica. Cuando se ejecuta la detección, la detección de redes no detecta los dispositivos SNMP con el nombre de comunidad especificado en la subred que se ha deshabilitado.  

####  <a name="BKMK_DetermineNetTopology"></a> Determinación de la topología de red  
 Puede utilizar una detección solo de topología para asignar unidades de red. Este tipo de detección no detecta posibles clientes. La detección de redes solo de topología se basa en SNMP.  

 Al asignar la topología de red, debe configurar el **Número máximo de saltos** en la pestaña **SNMP** del cuadro de diálogo **Propiedades de detección de redes**. Unos pocos saltos pueden ayudarle a controlar el ancho de banda de red que se utiliza cuando se ejecuta la detección. Conforme aumenta el número de elementos detectados en su red, puede incrementar el número de saltos para obtener una mejor comprensión de la topología de red.  

 Una vez que ha comprendido su topología de red, puede configurar propiedades adicionales para Detección de redes con el fin de detectar clientes potenciales y sus sistemas operativos mientras usa las configuraciones disponibles para limitar los segmentos de red que Detección de redes puede encontrar.  

####  <a name="BKMK_LimitBySubnet"></a> Limitación de búsquedas mediante el uso de subredes  
 Puede configurar Detección de redes para buscar subredes específicas durante la ejecución de la detección. De forma predeterminada, Detección de redes busca la subred del servidor que ejecuta la detección. Las subredes adicionales que se pueden configurar y habilitar solo se aplican a las opciones de búsqueda de SNMP y Protocolo de configuración dinámica de host (DHCP). Cuando Detección de redes busca dominios, no está limitada por las configuraciones para subredes.  

 Si especifica una o más subredes en la pestaña **Subredes** del cuadro de diálogo **Propiedades de detección de redes** , solo se buscarán las subredes marcadas como **Habilitada** .  

 Cuando se deshabilita una subred, esta se excluye de la detección y se aplican las condiciones siguientes:  

-   Las consultas basadas en SNMP no se ejecutan en la subred.  

-   Los servidores DHCP no responden con una lista de recursos ubicados en la subred.  

-   Las consultas basadas en dominio pueden detectar recursos ubicados en la subred.  

####  <a name="BKMK_SearchByDomain"></a> Búsqueda en un dominio específico  
 Puede configurar Detección de redes para buscar un dominio específico o un conjunto de dominios durante la ejecución de la detección. De forma predeterminada, Detección de redes busca el dominio local del servidor que ejecuta la detección.  

 Si especifica uno o más dominios en la pestaña **Dominios** del cuadro de diálogo **Propiedades de detección de redes** , solo se buscarán los dominios marcados como **Habilitado** .  

 Cuando se deshabilita un dominio, este se excluye de la detección y se aplican las condiciones siguientes:  

-   Detección de redes no consulta a los controladores de dominio de ese dominio.  

-   Las consultas basadas en SNMP pueden continuar ejecutándose en subredes del dominio.  

-   Los servidores DHCP pueden responder todavía con una lista de recursos ubicados en el dominio.  

####  <a name="BKMK_LimitBySNMPname"></a> Limitación de búsquedas mediante el uso de nombres de comunidad SNMP  
 Configure Detección de redes para buscar una comunidad SNMP específica o un conjunto de comunidades durante la ejecución de la detección. De forma predeterminada, el nombre de comunidad configurado para su uso es **public** .  

 Detección de redes utiliza nombres de comunidad para tener acceso a los enrutadores que son dispositivos SNMP. Un enrutador puede proporcionar Detección de redes con información acerca de otros enrutadores y subredes que están vinculados al primer enrutador.  

> [!NOTE]  
>  Los nombres de comunidad SNMP son similares a las contraseñas. Detección de redes puede obtener la información solo de un dispositivo SNMP para el que se ha especificado un nombre de comunidad. Cada dispositivo SNMP puede tener su propio nombre de comunidad, pero a menudo el mismo nombre de comunidad se comparte entre varios dispositivos. Además, la mayoría de los dispositivos SNMP tienen el nombre de comunidad predeterminado **public**. Pero algunas organizaciones eliminan el nombre de comunidad **public** de sus dispositivos como precaución de seguridad.  

 Si se muestran varias comunidades SNMP en la pestaña **SNMP** del cuadro de diálogo **Propiedades de detección de redes**, Detección de redes las busca en el orden en el que se muestran. Para ayudar a minimizar el tráfico generado por los intentos de ponerse en contacto con un dispositivo mediante el uso de nombres diferentes, asegúrese de que los nombres usados con más frecuencia se encuentren al comienzo de la lista.  

> [!NOTE]  
>  Además de utilizar el nombre de comunidad SNMP, puede especificar la dirección IP o el nombre resoluble de un dispositivo SNMP específico. Para ello, en la pestaña **Dispositivos SNMP** del cuadro de diálogo **Propiedades de detección de redes**.  

####  <a name="BKMK_SearchByDHCP"></a> Búsqueda en un servidor DHCP específico  
 Puede configurar Detección de redes para utilizar un servidor DHCP específico o varios servidores para detectar clientes DHCP durante la ejecución de la detección.  

 Detección de redes busca todos los servidores DHCP especificados en la pestaña **DHCP** del cuadro de diálogo **Propiedades de detección de redes** . Si un servidor DHCP concede la dirección IP al servidor que ejecuta la detección, se puede configurar la detección para buscar ese servidor DHCP. Para ello, active la casilla **Incluir el servidor DHCP configurado para que el servidor de sitio lo utilice**.  

> [!NOTE]  
>  Para configurar correctamente un servidor DHCP en Detección de redes, el entorno debe ser compatible con IPv4. No se puede configurar Detección de redes para utilizar un servidor DHCP en un entorno nativo de IPv6.  

###  <a name="BKMK_HowToConfigNetDisc"></a> Cómo configurar la detección de redes  
 Use los procedimientos siguientes para detectar en primer lugar solo la topología de red y, a continuación, configurar Detección de redes para detectar clientes potenciales mediante una o más de las opciones de Detección de redes disponibles.  

##### <a name="to-determine-your-network-topology"></a>Para determinar la topología de red  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Elija **Detección de redes** para el sitio donde quiera ejecutar la detección de redes.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

    -   En la pestaña **General**, active la casilla **Habilitar la detección de redes** y seleccione **Topología** en las opciones de **Tipo de detección**.  

    -   En la pestaña **Subredes**, active la casilla **Buscar subredes locales**.  

        > [!TIP]  
        >  Si conoce las subredes concretas que componen la red, puede desactivar la casilla **Buscar subredes locales** y usar el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif) para agregar las subredes concretas en las que quiere buscar. Para redes grandes, a menudo es mejor buscar sólo una o dos subredes al mismo tiempo para minimizar el uso de ancho de banda de red.  

    -   En la pestaña **Dominios**, active la casilla **Buscar dominio local**.  

    -   En la pestaña **SNMP** , use la lista desplegable **Número máximo de saltos** para especificar el número de saltos de enrutador que Detección de redes puede incorporar al asignar la topología.  

        > [!TIP]  
        >  Cuando asigne por primera vez la topología de red, configure pocos saltos del enrutador para minimizar el uso de ancho de banda de red.  

4.  En la pestaña **Programación**, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif) para configurar una programación para la ejecución de la detección de redes.  

    > [!NOTE]  
    >  No se puede asignar una configuración de detección diferente para separar programaciones de Detección de redes. Cada vez que se ejecuta Detección de redes, utiliza la configuración de detección actual.  

5.  Elija **Aceptar** para aceptar las configuraciones. Detección de redes se ejecuta a la hora programada.  

##### <a name="to-configure-network-discovery"></a>Para configurar Detección de redes  

1.  En la consola de Configuration Manager, elija **Administración** > **Configuración de jerarquía** y, luego, **Métodos de detección**.  

2.  Elija **Detección de redes** para el sitio donde quiera ejecutar la detección de redes.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

4.  Active la casilla **Habilitar la detección de redes** en la pestaña **General** y luego, en las opciones de **Tipo de detección**, seleccione el tipo de detección que quiere ejecutar.  

5.  Para configurar la detección para la búsqueda de subredes, elija la pestaña **Subredes** y configure una o más de las opciones siguientes:  

    -   Para ejecutar la detección de subredes locales en el equipo que ejecuta la detección, active la casilla **Buscar subredes locales**.  

    -   Para buscar una subred específica, la subred debe aparecer en **Subred a buscar** y tener un valor de **Búsqueda** de **Habilitada**:  

        1.  Si la subred no aparece, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nueva asignación de subred**, escriba la información **Subred** y **Máscara** y luego elija **Aceptar**. De forma predeterminada, se habilita una nueva subred para la búsqueda.  

        2.  Para cambiar el valor de **Búsqueda** de una subred de la lista, seleccione la subred y elija el icono **Alternar** para alternar el valor entre **Deshabilitada** y **Habilitada**.  

6.  Para configurar la detección para la búsqueda de dominios, elija la pestaña **Dominios** y configure una o más de las opciones siguientes:  

    -   Para ejecutar la detección en el dominio del equipo que ejecuta la detección, active la casilla **Buscar dominio local**.  

    -   Para buscar un dominio concreto, el dominio debe aparecer en **Dominios** y tener un valor de **Búsqueda** de **Habilitada**:  

        1.  Si el dominio no aparece, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Propiedades del dominio**, escriba la información de **Dominio** y elija **Aceptar**. De forma predeterminada, se habilita un nuevo dominio para la búsqueda.  

        2.  Para cambiar el valor de **Búsqueda** de un dominio de la lista, seleccione el dominio y elija el icono **Alternar** para alternar el valor entre **Deshabilitada** y **Habilitada**.  

7.  Para configurar la detección para la búsqueda de nombres de comunidad SNMP específicos para dispositivos SNMP, elija la pestaña **SNMP** y configure una o más de las opciones siguientes:  

    -   Para agregar un nombre de comunidad SNMP a la lista **Nombres de comunidades SNMP**, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nombre de comunidad SNMP nuevo**, especifique el **Nombre** de la comunidad SNMP y elija **Aceptar**.  

    -   Para quitar un nombre de comunidad SNMP, seleccione el nombre de comunidad y elija el icono **Eliminar** ![icono Eliminar](media/Disc_delete_Icon.gif).  

    -   Para ajustar el orden de búsqueda de nombres de comunidades SNMP, seleccione un nombre de comunidad y elija el icono **Subir elemento** ![icono Subir elemento](media/Disc_moveUp_Icon.gif) o el icono **Bajar elemento** ![icono Bajar elemento](media/Disc_moveDown_Icon.gif). Cuando se ejecuta la detección, los nombres de comunidad se buscan de arriba a abajo. Tenga en cuenta los siguientes aspectos.

        > [!NOTE]  
        >  Detección de redes utiliza nombres de comunidad SNMP para tener acceso a los enrutadores que son dispositivos SNMP. Un enrutador puede informar a Detección de redes acerca de otros enrutadores y subredes vinculadas al primer enrutador.  

        -   Los nombres de comunidad SNMP son similares a las contraseñas.  

        -   Detección de redes puede obtener la información solo de un dispositivo SNMP para el que se ha especificado un nombre de comunidad.  

        -   Cada dispositivo SNMP puede tener su propio nombre de comunidad, pero a menudo el mismo nombre de comunidad se comparte entre varios dispositivos.  

        -   La mayoría de los dispositivos SNMP tienen el nombre de comunidad predeterminado **Public**. Puede usarlo si no conoce ningún otro nombre de comunidad. Sin embargo, algunas organizaciones eliminan el nombre de comunidad **Public** de sus dispositivos como precaución de seguridad.  

8.  Para configurar el número máximo de saltos de enrutador en las búsquedas de SNMP, elija la pestaña **SNMP** y seleccione el número de saltos en la lista desplegable **Número máximo de saltos**.  

9. Para configurar un dispositivo SNMP, elija la pestaña **Dispositivos SNMP**. Si el dispositivo no aparece, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Nuevo dispositivo SNMP**, especifique la dirección IP o el nombre del dispositivo SNMP y elija **Aceptar**.  

    > [!NOTE]  
    >  Si especifica un nombre de dispositivo, Configuration Manager debe ser capaz de resolver el nombre NetBIOS en una dirección IP.  

10. Para configurar la detección para la consulta de servidores DHCP específicos para clientes DHCP, elija la pestaña **DHCP** y configure una o más de las opciones siguientes:  

    -   Para consultar el servidor DHCP en el equipo que ejecuta la detección, active la casilla **Usar siempre el servidor DHCP del servidor de sitio**.  

        > [!NOTE]  
        >  Para utilizar esta opción, el servidor debe conceder su dirección IP desde un servidor DHCP y no puede utilizar una dirección IP estática.  

    -   Para consultar un servidor DHCP específico, elija el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif). En el cuadro de diálogo **Servidor DHCP nuevo**, especifique la dirección IP o el nombre del servidor y luego elija **Aceptar**.  

        > [!NOTE]  
        >  Si especifica un nombre de servidor, Configuration Manager debe ser capaz de resolver el nombre NetBIOS en una dirección IP.  

11. Para configurar cuándo se va a ejecutar la detección, elija la pestaña **Programación** y luego, el icono **Nuevo** ![icono Nuevo](media/Disc_new_Icon.gif) para establecer una programación para ejecutar la detección de redes.  

     Puede configurar varias programaciones periódicas y programaciones sin ninguna periodicidad.  

    > [!NOTE]  
    >  Si se aparecen varias programaciones en la pestaña **Programación** a la vez, todas las programaciones ejecutarán una Detección de redes conforme a la configuración y a la hora indicada en la programación. Esto también se aplica a las programaciones periódicas.  

12. Elija **Aceptar** para guardar las configuraciones.  

###  <a name="BKMK_HowToVerifyNetDisc"></a> Cómo comprobar que se ha completado la detección de redes  
 El tiempo necesario para que finalice la detección de redes puede variar en función de diversos factores. Estos factores pueden incluir uno o varios de los siguientes:  

-   El tamaño de la red  

-   La topología de la red  

-   El número máximo de saltos que están configurados para buscar enrutadores en la red  

-   El tipo de detección que se está ejecutando  

Debido a que Detección de redes no crea mensajes para alertarle del momento en que ha finalizado la detección, puede utilizar el siguiente procedimiento para comprobar cuándo ha finalizado la detección.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Para comprobar que ha finalizado la detección de redes  

1.  En la consola de Configuration Manager, elija **Supervisión**.  

2.  En el área de trabajo **Supervisión**, expanda **Estado del sistema** y elija **Consultas de mensaje de estado**.  

3.  Elija **Todos los mensajes de estado**.  

4.  En el grupo **Consultas de mensaje de estado** de la pestaña **Inicio**, elija **Mostrar mensajes**.  

5.  En la lista desplegable **Seleccionar fecha y hora**, seleccione un valor que incluya el momento en que se inició la detección y, luego, elija **Aceptar** para abrir el **Visor de mensajes de estado de Configuration Manager**.  

    > [!TIP]  
    >  También puede usar la opción **Especificar fecha y hora** para seleccionar la fecha y la hora de ejecución de la detección. Esta opción es útil cuando se ejecuta la detección de redes en una determinada fecha y desea recuperar los mensajes solo desde esa fecha.  

6.  Para validar la finalización de la detección de redes, busque un mensaje de estado que tenga los siguientes detalles:  

    -   Id. de mensaje: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descripción: **Este componente se detuvo**  

    Si este mensaje de estado no aparece, la detección de redes no ha terminado.  

7.  Para validar el inicio de la detección de redes, busque un mensaje de estado con los detalles siguientes:  

    -   Id. de mensaje: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descripción: **Este componente se inició**  

    Esta información comprueba el inicio de la detección de redes. Si esta información no aparece, vuelva a programar la detección de redes.  

