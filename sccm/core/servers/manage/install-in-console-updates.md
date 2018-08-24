---
title: Actualización en la consola
titleSuffix: Configuration Manager
description: Instalación de actualizaciones en Configuration Manager desde Microsoft Cloud
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ea03f3a91d086a3528047ac6fcd18ff09b03537
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385565"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Instalar actualizaciones en consola para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Configuration Manager se sincroniza con el servicio de Microsoft Cloud para obtener actualizaciones. Después, puede instalar estas actualizaciones desde la consola de Configuration Manager.



## <a name="get-available-updates"></a>Obtención de actualizaciones disponibles

El sitio solo descargará actualizaciones válidas para su infraestructura y versión. Esta sincronización puede ser automática o manual, según cómo configure el punto de conexión de servicio para la jerarquía:

-   En **modo en línea**, el punto de conexión de servicio se conecta al servicio en la nube de Microsoft automáticamente y descarga las actualizaciones aplicables.  

     De manera predeterminada, Configuration Manager busca nuevas actualizaciones cada 24 horas. Busque actualizaciones de forma manual en la consola de Configuration Manager. Vaya al área de trabajo **Administración**, seleccione el nodo **Actualizaciones y mantenimiento** y, después, haga clic en **Buscar actualizaciones** en la cinta de opciones.  

-   En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft. Para descargar y luego importar las actualizaciones disponibles, puede [usar la herramienta de conexión de servicio](/sccm/core/servers/manage/use-the-service-connection-tool).  

> [!NOTE]  
> Si es necesario, puede importar correcciones fuera de banda en la consola. Para ello, use la [herramienta de registro de actualizaciones](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Estas correcciones fuera de banda complementan las actualizaciones que obtendrá al sincronizar con el servicio de Microsoft Cloud.  


Cuando se sincronicen las actualizaciones, podrá verlas en la consola de Configuration Manager. Vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**.  

-   Las actualizaciones no instaladas se muestran con el estado **Disponible**.  

-   Las actualizaciones instaladas se muestran con el estado **Instalada**. Solo se muestra la última actualización instalada. Haga clic en el botón **Historial** de la cinta de opciones para ver las actualizaciones instaladas anteriormente.  


Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus usos adicionales. Los usos siguientes pueden afectar al modo en que se configura este rol de sistema de sitio:  

-   El punto de conexión de servicio se usa para cargar la información de uso sobre su sitio. Esta información ayuda al servicio en la nube de Microsoft a identificar las actualizaciones que están disponibles para la versión actual de su infraestructura. Para obtener más información, vea [Diagnósticos y datos de uso](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

-   El sitio usa el punto de conexión de servicio para administrar dispositivos con Microsoft Intune y con la administración de dispositivos móviles local de Configuration Manager. Para obtener más información, vea [Administración de dispositivos móviles (MDM) híbrida](/sccm/mdm/understand/hybrid-mobile-device-management).  

Para entender mejor lo que ocurre cuando se descargan las actualizaciones, vea los siguientes diagramas de flujo:  

-   [Diagrama de flujo: descargar actualizaciones](/sccm/core/servers/manage/download-updates-flowchart)  

-   [Diagrama de flujo: replicación de actualización](/sccm/core/servers/manage/update-replication-flowchart)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Asignar permisos para ver y administrar actualizaciones y características

Para que un usuario vea las actualizaciones en la consola, debe tener asignado un rol de seguridad de administración basado en roles que incluya la clase de seguridad **Paquetes de actualización**. Esta clase concede acceso para ver y administrar las actualizaciones en la consola de Configuration Manager.    


#### <a name="about-the-update-packages-class"></a>Sobre la clase Paquetes de actualización   
De forma predeterminada, la clase **Paquetes de actualización** (SMS_CM_Updatepackages) forma parte de los siguientes roles de seguridad integrados con los permisos indicados:  

-  **Administrador total** con permisos **Modificar** y **Lectura** :  

    -   Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Todo** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación y habilitar características individuales cuando se actualice el sitio.  

    - Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Predeterminado** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación y ver características cuando se actualice el sitio. Pero este usuario no podrá habilitar las características cuando se actualice el sitio.  

- **Analista de solo lectura** con permisos **Lectura** :  

  -  Un usuario con este rol de seguridad y acceso al ámbito **Predeterminado** puede ver actualizaciones pero no instalarlas. Este usuario también podrá ver características después de actualizar el sitio, pero no podrá habilitarlas.  


#### <a name="permissions-required-for-updates-and-servicing"></a>Permisos necesarios para las actualizaciones y el mantenimiento   
- Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y los permisos **Modificar** y **Lectura**.  

- Asigne la cuenta al ámbito **Predeterminado**.  

#### <a name="permissions-to-only-view-updates"></a>Permisos para solo ver las actualizaciones   
- Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y que tenga solo con el permiso **Lectura**.  

- Asigne la cuenta al ámbito **Predeterminado**.  

#### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Permisos necesarios para habilitar características cuando se actualice el sitio   
-  Use una cuenta que tenga asignado un rol de seguridad con la clase **Paquetes de actualización** y los permisos **Modificar** y **Lectura**.  

-  Asigne la cuenta al ámbito **Todo**.  



##  <a name="bkmk_beforeinstall"></a> Antes de instalar una actualización en la consola  

Revise los pasos siguientes antes de instalar una actualización desde la consola de Configuration Manager.  


###  <a name="bkmk_step1"></a> Paso 1: Revisar la lista de comprobación de actualización  

Revise la lista de comprobación de actualización aplicable para las acciones que deben realizarse antes de iniciar la actualización:

- [Lista de comprobación para la instalación de la actualización 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806)  

- [Lista de comprobación para la instalación de la actualización 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802)

- [Lista de comprobación para la instalación de la actualización 1710](/sccm/core/servers/manage/checklist-for-installing-update-1710)  


###  <a name="bkmk_step2"></a> Paso 2: Ejecutar el comprobador de requisitos previos antes de instalar una actualización  

Antes de instalar una actualización, puede ejecutar la comprobación de requisitos previos para la actualización. Si ejecuta la comprobación de requisitos previos antes de instalar una actualización:  

-   Los archivos de actualización se replican en otros sitios antes de instalar la actualización.  

-   La comprobación de requisitos previos se volverá a ejecutar automáticamente cuando instale la actualización.  

> [!NOTE]   
> Al iniciar una comprobación de requisitos previos y, después, ver el estado, parecerá que la fase **Instalación** está activa. Pero, en realidad, no se instalará la actualización en el sitio. Para ejecutar la comprobación de requisitos previos, el proceso de actualización extrae el paquete de la biblioteca de contenido. Después, copia el paquete en una carpeta de almacenamiento provisional, donde puede acceder a las comprobaciones de requisitos previos actuales. El mismo proceso también se ejecuta al instalar una actualización. Este comportamiento se debe a que la fase de instalación se muestra con el estado **En curso**. En la categoría de instalación solo se muestra el paso *Extraer paquete de actualización*.  

Más adelante, cuando instale la actualización, puede configurarla para omitir las advertencias de comprobación de requisitos previos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para ejecutar el Comprobador de requisitos previos antes de instalar una actualización  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**.   

2.  Haga clic con el botón derecho en el paquete de actualización para el que quiera ejecutar la comprobación de requisitos previos.  

3.  Haga clic en **Ejecutar comprobación de requisitos previos** en la cinta de opciones.  

     Cuando se ejecuta la comprobación de requisitos previos, el contenido de la actualización se replica a los sitios secundarios. Puede ver el archivo **distmgr.log** en el servidor de sitio para confirmar que el contenido se replique correctamente.  

4.  Para ver los resultados de la comprobación de requisitos previos:  

    1. En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**.  

    2. Seleccione el nodo **Actualizaciones y estado de mantenimiento** y busque el estado de los requisitos previos.  

    3. Para obtener más información, vea el archivo **ConfigMgrPrereq.log** en el servidor de sitio.  



##  <a name="bkmk_install"></a> Instalación de actualizaciones en la consola  

Cuando esté listo para instalar actualizaciones en la consola de Configuration Manager, empiece con el sitio de primer nivel de la jerarquía. Este sitio puede ser el sitio de administración central o un sitio primario independiente.  

Le recomendamos que instale la actualización fuera del horario comercial habitual para cada sitio con el fin de minimizar el efecto sobre las operaciones empresariales. El motivo es que, al instalar actualizaciones, pueden realizarse acciones como la reinstalación de componentes de sitio y roles del sistema de sitio.  

-   Los sitios primarios secundarios inician la actualización automáticamente cuando el sitio de administración central termina de instalarla. Este es el proceso recomendado y predeterminado. Para controlar el momento en que un sitio primario instala actualizaciones, use [Períodos para tareas administrativas para servidores de sitios](/sccm/core/servers/manage/service-windows).  

-   Cuando se complete la actualización del sitio principal primario, actualice de forma manual los sitios secundarios desde la consola de Configuration Manager. No se admite la actualización automática de los servidores de sitio secundario.  

-   Cuando se usa una consola de Configuration Manager después de actualizar el sitio, también se le pide que actualice la consola.  

-  Después de que el servidor de sitio completa correctamente la instalación de una actualización, actualiza automáticamente todos los roles de sistema de sitio aplicables. Pero no se reinstalan todos los puntos de distribución y pasan a estar sin conexión para actualizar al mismo tiempo. En su lugar, el servidor de sitio usa la configuración de distribución de contenido del sitio para distribuir la actualización a un subconjunto de puntos de distribución a la vez. El resultado es que solo algunos puntos de distribución se desconectan para instalar la actualización. Los puntos de distribución que todavía no han empezado a actualizarse o que han completado la actualización permanecen en línea y pueden proporcionar contenido a los clientes.


###  <a name="bkmk_overview"></a> Información general sobre la instalación de actualizaciones en la consola  

#### <a name="1-when-the-update-installation-starts"></a>1. Cuando se inicia la instalación de la actualización  
Verá el asistente para actualizaciones, donde se muestra una lista de las áreas de producto que se corresponden con la actualización.  

-   En la página **General** del asistente, puede configurar **Advertencias de requisitos previos** según sea necesario:  

    -   Los errores de requisitos previos siempre detienen la instalación de la actualización. Solucione los errores para poder reintentar la instalación de la actualización de manera satisfactoria. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry).  

    -   Las advertencias de requisitos previos también pueden detener la instalación de la actualización. Solucione las advertencias antes de reintentar la instalación de la actualización. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry).  

    -   **Pase por alto las advertencias de las comprobaciones de requisitos previos e instale esta actualización aunque falten requisitos**: establece una condición para la instalación de actualizaciones que omite las advertencias de requisitos previos. Esta opción permite continuar con la instalación de la actualización. Si no selecciona esta opción, la instalación de actualizaciones se detiene cuando el proceso se encuentra una advertencia. A menos que ya haya ejecutado anteriormente la comprobación de requisitos previos y haya resuelto las advertencias de requisitos previos para un sitio, no le recomendamos que use esta opción.  

      En las áreas de trabajo **Administración** y **Supervisión**, el nodo Actualizaciones y mantenimiento tiene un botón en la cinta de opciones denominado **Omitir advertencias de requisitos previos**. Este botón está disponible cuando se produce un error al completar la instalación de un paquete de actualización debido a las advertencias de comprobación de los requisitos previos. Por ejemplo, instale una actualización sin utilizar la opción para ignorar las advertencias de requisitos previos (desde el Asistente para actualizaciones). La instalación de actualización se detiene con un estado de advertencia de requisitos previos, pero sin errores. Más tarde, haga clic en **Omitir advertencias de requisitos previos** en la cinta de opciones. Esta acción desencadena una continuación automática de esa instalación de actualizaciones que omite las advertencias de requisitos previos. Cuando se usa esta opción, la instalación de la actualización continúa automáticamente después de unos minutos.  


-   Si hay una actualización válida para el cliente de Configuration Manager, pruebe la actualización de cliente con un conjunto limitado de clientes. Para obtener más información, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción](/sccm/core/clients/manage/upgrade/test-client-upgrades).  


#### <a name="2-during-the-update-installation"></a>2. Durante la instalación de la actualización  
Como parte de la instalación de actualizaciones, Configuration Manager realiza las acciones siguientes:  

-   Vuelve a instalar los componentes afectados, como los roles de sistema de sitio o la consola de Configuration Manager.  

-   Administra las actualizaciones de los clientes en función de las selecciones realizadas para las comprobaciones piloto de clientes y para las [actualizaciones de cliente automáticas](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

-   Normalmente, los servidores de sistema de sitio no necesitan reiniciarse como parte de la actualización. Si un rol usa .NET y el paquete actualiza ese componente de requisitos previos, puede que se reinicie el sistema de sitio.  

> [!TIP]  
>  Al instalar actualizaciones de Configuration Manager, el sitio también actualiza la carpeta CD.Latest. Para obtener más información, vea [La carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Supervisar el progreso de las actualizaciones mientras se instalan  
Para supervisar el progreso, siga este procedimiento:  

-   En la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. En este nodo se muestra el estado de instalación de todos los paquetes de actualización.  

-   En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y seleccione el nodo **Actualizaciones y estado de mantenimiento**. En este nodo, solo se muestra el estado de la instalación del paquete de actualización que el sitio esté instalando.  

    La instalación de actualizaciones se divide en varias fases para facilitar la supervisión. Por cada una de las fases siguientes, en los detalles adicionales del estado de la instalación, se indica qué archivo de registro contiene más información:  

    -   **Descarga**: esta fase solo se aplica en el sitio de primer nivel con el punto de conexión de servicio.   

    -   **replicación**   

    -   **Comprobación de requisitos previos**   

    -   **Instalación**    

    -   **Después de la instalación**: para obtener más información, vea [Tareas posteriores a la instalación](#post-installation-tasks).  

-   Vea el archivo **CMUpdate.log** en `<ConfigMgr_Installation_Directory>\Logs` en el servidor de sitio.  


#### <a name="4-when-the-update-installation-completes"></a>4. Cuando se completa la instalación de la actualización  
Después de que se completa la primera actualización del sitio:  

-   Los sitios primarios secundarios instalan la actualización automáticamente. No es necesario hacer nada.  

-   Necesita actualizar manualmente los sitios secundarios desde la consola de Configuration Manager. Para obtener más información, vea [Iniciar la instalación de actualizaciones en un sitio secundario](#bkmk_secondary).  

-   Hasta el momento en que todos los sitios de la jerarquía estén actualizados a la nueva versión, la jerarquía funciona en modo de versión mixta. Para obtener más información, vea [Interoperabilidad entre diferentes versiones](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Actualizar consolas de Configuration Manager  
Cuando se actualice un sitio de administración central o un sitio primario, también tendrán que actualizarse todas las consolas de Configuration Manager que se conecten a ese sitio. Se le pedirá que actualice una consola:  

-   Cuando abre la consola.  

-   Cuando se desplaza a un nuevo nodo en una consola abierta.  

Actualice la consola inmediatamente después de que se actualice el sitio.  

Cuando se actualice la consola, compruebe que la versión de la consola y del sitio sean correctas. Vaya a **Acerca de System Center Configuration Manager** en la esquina superior izquierda de la consola.  

 > [!Note]  
 > A partir de la versión 1802, la versión de la consola ahora es ligeramente diferente de la versión del sitio. La versión secundaria de la consola ahora corresponde a la versión de lanzamiento de Configuration Manager. Por ejemplo, en Configuration Manager versión 1802, la versión de sitio inicial es 5.0.8634.1000 y la versión inicial de la consola es 5. **1802**.1082.1700. Los números de compilación (1082) y revisión (1700) pueden cambiar con futuras revisiones de la versión 1802.



###  <a name="bkmk_toptier"></a> Para iniciar la instalación de actualizaciones en el sitio de primer nivel  

En el sitio de primer nivel de la jerarquía, en la consola de Configuration Manager, vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. Seleccione una actualización con el estado **Disponible** y, después, haga clic en **Instalar el paquete de actualización** en la cinta de opciones.  


###  <a name="bkmk_secondary"></a> Para iniciar la instalación de la actualización en un sitio secundario  

Cuando se actualice el sitio primario principal de un sitio secundario, actualice el sitio secundario desde la consola de Configuration Manager. Para ello, utilice el **Asistente para actualizar sitios secundarios**.  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio secundario que quiera actualizar y, después, haga clic en **Actualizar** en la cinta de opciones.  

2.  Haga clic en **Sí** para iniciar la actualización del sitio secundario.  

Para supervisar la instalación de actualizaciones en un sitio secundario, seleccione el sitio secundario y haga clic en **Mostrar estado de instalación** en la cinta de opciones. También puede agregar la columna **Versión** al nodo Sitios para ver la versión de cada sitio secundario.  

En algunos casos, el estado de la consola no se actualiza ni sugiere que la actualización produce errores. Después de actualizar correctamente un sitio secundario, use la opción **Volver a intentar la instalación**. Esta opción no reinstala la actualización del sitio secundario que instaló correctamente la actualización, sino que obliga a la consola a actualizar el estado.


### <a name="post-installation-tasks"></a>Tareas posteriores a la instalación

Cuando un sitio instala una actualización, hay varias tareas que no se pueden iniciar hasta que la actualización finalice la instalación en el servidor de sitio. Esta lista contiene las tareas posteriores a la instalación que son críticas para las operaciones de sitio y jerarquía. Como son críticas, se supervisan activamente. Entre las tareas adicionales que no se supervisan directamente, se encuentra la reinstalación de los roles de sistema de sitio. Para ver el estado de las tareas críticas posteriores a la instalación, seleccione la tarea **Postinstalación** durante la supervisión de la instalación de actualizaciones para un sitio.

No todas las tareas se completan de inmediato. Algunas tareas no se inician hasta que cada sitio complete la instalación de la actualización. La nueva funcionalidad que cabría esperar puede retrasarse hasta que se completen estas tareas. La activación de nuevas características no se inicia hasta que todos los sitios completen la instalación de actualizaciones, por lo que es posible que las nuevas características no estén visibles durante algún tiempo.

Entre las tareas posteriores a la instalación figuran las siguientes:

-   **Instalación del servicio SMS_EXECUTIVE**
  -   Servicio crítico que se ejecuta en el servidor de sitio.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Subproceso de componente de sitio crítico del servicio SMS_EXECUTIVE.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_HIERARCHY_MANAGER**
  -   Componente de sitio crítico que se ejecuta en el servidor de sitio.
  -   Responsable de la reinstalación de los roles de sistema de sitio en los servidores de sistema de sitio. No se muestra el estado de la reinstalación del rol de sistema de sitio individual.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de sitio crítico que se ejecuta en el servidor de sitio.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_POLICY_PROVIDER**
  -   Componente de sitio crítico que se ejecuta solo en sitios primarios.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Supervisando inicialización de replicación**   
  -   Esta tarea se muestra solo en el sitio de administración central y los sitios primarios secundarios.
  -   Depende de SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Debe completarse rápidamente.


-   **Actualizando el paquete de preproducción del cliente de Configuration Manager**    
  -   Esta tarea se muestra incluso cuando la preproducción del cliente (también llamada piloto de cliente) no está habilitada para su uso.
  -   No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.


-   **Actualizando la carpeta Client en el servidor de sitio**
  -   Esta tarea no se muestra si usa el cliente en preproducción.  
  -   Debe completarse rápidamente.


-   **Actualizando el paquete del cliente de Configuration Manager**
  -   Esta tarea no se muestra si usa el cliente en preproducción.  
  -   Finaliza solo después de que todos los sitios instalan la actualización.  


-   **Activación de características**
  -   Esta tarea se muestra únicamente en el sitio de nivel superior de la jerarquía.
  -   No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.
  -   No se muestran las características individuales.



##  <a name="bkmk_retry"></a> Reintento de la instalación de una actualización con errores  

Si no puede instalar una actualización, revise los comentarios en la consola para identificar las soluciones de errores y las advertencias. Para obtener más información, vea el archivo **ConfigMgrPrereq.log** en el servidor de sitio. Antes de reintentar la instalación de una actualización, debe solucionar los errores y las advertencias.  

> [!TIP]  
> Si una actualización tiene problemas de descarga o replicación, use la [herramienta de restablecimiento de actualizaciones](/sccm/core/servers/manage/update-reset-tool).  

Cuando esté listo para reintentar la instalación de una actualización, seleccione la actualización con errores y elija una opción adecuada. El comportamiento del reintento de instalación de la actualización depende del nodo desde el que se inicia el reintento y de la opción de reintento que se usa.  

#### <a name="retry-installation-for-the-hierarchy"></a>Volver a intentar la instalación en la jerarquía
Puede volver a intentar la instalación de una actualización en toda la jerarquía si la actualización se encuentra en alguno de los estados siguientes:  

  -   Las comprobaciones de requisitos previos se han superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualización de **Ignorar advertencia sobre requisitos previos** en el nodo **Actualizaciones y mantenimiento** es **No**).   

  -   Errores en la comprobación de requisitos previos    

  -   Error de instalación  

  -   Error en la replicación del contenido en el sitio   

Vaya al área de trabajo **Administración** y seleccione el nodo **Actualizaciones y mantenimiento**. Seleccione la actualización y, después, elija una de estas opciones:  

  -   **Reintentar**: al **Reintentar** desde **Actualizaciones y mantenimiento**, la instalación de la actualización vuelve a empezar y omite automáticamente las advertencias de requisitos previos. Si la réplica de contenido ha producido errores anteriormente, el contenido de la actualización se volverá a replicar.  

  - **Omitir advertencias de requisitos previos**: si se detiene la instalación de la actualización debido a una advertencia, puede seleccionar **Omitir advertencias de requisitos previos**. Esta acción permite que la instalación de la actualización continúe en unos minutos y usa la opción para omitir las advertencias de requisitos previos.   

#### <a name="retry-installation-for-the-site"></a>Volver a intentar la instalación en el sitio  
Puede reintentar la instalación de una actualización en un sitio específico si la actualización se encuentra en alguno de los estados siguientes:  

  -   Las comprobaciones de requisitos previos se han superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualizaciones de **Ignorar advertencia sobre requisitos previos** en el nodo Actualizaciones y mantenimiento es **No**).  

  -   Errores en la comprobación de requisitos previos    

  -   Error de instalación    

Vaya al área de trabajo **Supervisión** y seleccione el nodo **Estado de mantenimiento del sitio**. Seleccione la actualización y, después, haga clic en una de las opciones siguientes:  

  - **Reintentar**: al **Reintentar** desde **Estado de mantenimiento del sitio**, se reinicia la instalación de la actualización solo en ese sitio. A diferencia de ejecutar **Reintentar** en el nodo **Actualizaciones y mantenimiento**, este reintento no omite las advertencias de requisitos previos.  

  - **Omitir advertencias de requisitos previos**: si se detiene la instalación de la actualización debido a una advertencia, puede hacer clic en **Omitir advertencias de requisitos previos**. Esta acción permite que la instalación de la actualización continúe en unos minutos y usa la opción para omitir las advertencias de requisitos previos.  



##  <a name="bkmk_after"></a> Después de que un sitio instala una actualización  

Use la siguiente lista de comprobación para completar tareas comunes y configuraciones que se realizan después de actualizar un sitio.   

#### <a name="confirm-site-to-site-replication-is-active"></a>Confirmar que la replicación de sitio a sitio está activa
En la consola de Configuration Manager, vaya a las ubicaciones siguientes para ver el estado y asegurarse de que la replicación esté activa:  

-   Área de trabajo **Supervisión**, nodo **Jerarquía de sitios**  

-   Área de trabajo **Supervisión**, **nodo Replicación de base de datos**  

Vea los siguientes artículos para más información:  
- [Supervisar la infraestructura de la jerarquía y replicación](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [Información sobre Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  

#### <a name="confirm-that-servers-restarted-if-necessary"></a>Confirmar que los servidores se hayan reiniciado (si es necesario) 
Revise la infraestructura del sitio y asegúrese de que los servidores de sitios y los servidores de sistema de sitio remoto se hayan reiniciado correctamente. Normalmente, los servidores de sitio se reinician solo si Configuration Manager instala .NET como un requisito previo para un rol de sistema de sitio.  

#### <a name="update-standalone-configuration-manager-consoles"></a>Actualizar las consolas independientes de Configuration Manager
Actualice todas las consolas de Configuration Manager remotas a la misma versión. Se le pedirá que actualice la consola:  

-   Cuando se desplaza a un nuevo nodo en la consola.  

-   Cuando abre la consola.  

#### <a name="reconfigure-database-replicas-for-management-points"></a>Volver a configurar réplicas de base de datos para puntos de administración
Si usa réplicas de base de datos para puntos de administración en sitios primarios, necesita desinstalar las réplicas de base de datos antes de actualizar el sitio. Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración. Para obtener más información, vea [Réplicas de bases de datos para puntos de administración ](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Volver a configurar las tareas de mantenimiento deshabilitadas
Si ha deshabilitado las [tareas de mantenimiento](/sccm/core/servers/manage/maintenance-tasks) de bases de datos en un sitio antes de instalar la actualización, vuelva a configurar esas tareas en el sitio. Use la misma configuración que había antes de la actualización.  

#### <a name="upgrade-clients"></a>Actualizar clientes.
Para obtener más información, vea [Actualizar clientes para equipos con Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  

#### <a name="additional-configurations"></a>Configuraciones adicionales
Revise los cambios realizados antes de iniciar la actualización y, después, restaure esas configuraciones a sus sitios y jerarquías.  



##  <a name="bkmk_options"></a> Habilitar características opcionales de las actualizaciones  

Cuando una actualización incluye una o varias características opcionales, tiene la oportunidad de habilitar esas características en la jerarquía. Puede habilitar características cuando se instale la actualización, o bien puede volver a la consola posteriormente y habilitar las características opcionales.

Para ver las características disponibles y su estado, en la consola, vaya al área de trabajo **Administración**, expanda **Actualizaciones y mantenimiento** y, después, seleccione el nodo **Características**.

Cuando una característica no es opcional, se instala automáticamente. No aparece en el nodo **Características**.  

> [!Important]  
> En una jerarquía multisitio, solo se pueden habilitar características opcionales o de versión preliminar desde el sitio de administración central. Con este comportamiento se procura que no haya ningún conflicto en la jerarquía. <!--507197-->
 

Al habilitar una característica nueva o de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. El procesamiento del cambio suele ser inmediato. Según el ciclo de procesamiento de HMAN, puede tardar hasta 30 minutos en completarse. Una vez procesado el cambio, reinicie la consola antes de usar la característica.

#### <a name="list-of-optional-features"></a>Lista de características opcionales
Las siguientes características son opcionales en la versión más reciente de Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

-->

- [Alta disponibilidad de servidor de sitio](/sccm/core/servers/deploy/configure/site-server-high-availability)<!--1128774-->
- [Actualizaciones de software de terceros](/sccm/sum/deploy-use/third-party-software-updates)<!--1357605,1352101,1358714-->
- [Aprobación de solicitudes de aplicación para los usuarios por dispositivo](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  
- [Compatibilidad con Cisco AnyConnect 4.0.07x y versiones posteriores para iOS](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393-->
- [Evaluación de Atestación de estado de dispositivo para las directivas de cumplimiento de acceso condicional](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Creación y ejecución de scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Ejecutar paso de secuencia de tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Almacenamiento en caché previa de contenido de secuencias de tareas](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Actualizaciones de controladores de Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Punto de servicio de almacenamiento de datos](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Caché del mismo nivel de cliente](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Creación de PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Conector de Microsoft Operations Management Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [Directiva de Protección contra vulnerabilidades de seguridad de Windows Defender](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [VPN para Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (conocido ahora como *Windows Hello para empresas*) <!--1245704-->
- [Acceso condicional para los equipos administrados](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->


> [!Tip]  
> Para obtener más información sobre las características cuya habilitación requiere consentimiento, consulte las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features).  
> 
> Para más información sobre las características que solo están disponibles en la rama de Technical Preview, vea [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Uso de las características de versión preliminar de las actualizaciones

Las características de versión preliminar se incluyen en la Rama actual para realizar pruebas anticipadamente en un entorno de producción. Para obtener más información, vea [Características de versión preliminar](/sccm/core/servers/manage/pre-release-features).



## <a name="bkmk_faq"></a> Preguntas más frecuentes

###  <a name="why-dont-i-see-certain-updates-in-my-console"></a>¿Por qué no se ven determinadas actualizaciones en la consola?  

Si no encuentra una actualización específica en la consola después de una sincronización correcta con el servicio en la nube de Microsoft, este comportamiento podría deberse a uno de los motivos siguientes:  

-   La actualización necesita una configuración que no usa la infraestructura, o bien la versión del producto actual no cumple un requisito previo para recibir la actualización.  

     Si cree que tiene las configuraciones necesarias y otros requisitos previos para una actualización que falta, confirme que su punto de conexión de servicio se encuentre en el modo en línea. Después, use la opción **Buscar actualizaciones** en el nodo **Actualizaciones y mantenimiento** para forzar una comprobación. Cuando el punto de conexión de servicio está en el modo sin conexión, se usa la herramienta de conexión de servicio para ejecutar manualmente la sincronización con el servicio en la nube.  

-   La cuenta no dispone de los permisos de administración basada en roles correctos para ver las actualizaciones en la consola de Configuration Manager. Para obtener más información, vea [Permisos para administrar actualizaciones](#assign-permissions-to-view-and-manage-updates-and-features).  

