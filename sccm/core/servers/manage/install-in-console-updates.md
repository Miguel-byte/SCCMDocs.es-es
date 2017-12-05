---
title: "Actualización en la consola"
titleSuffix: Configuration Manager
description: System Center Configuration Manager se sincroniza con la nube de Microsoft para obtener las actualizaciones que puede instalar desde la consola.
ms.custom: na
ms.date: 09/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: "36"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 081935ebb3ef2cc12d2023d86c0b68bbd816f2f3
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/04/2017
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Instalación de actualizaciones en la consola para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager se sincroniza con el servicio en la nube de Microsoft para obtener actualizaciones. Después, puede instalarlas desde la consola de Configuration Manager.

## <a name="get-available-updates"></a>Obtención de actualizaciones disponibles
Solo las actualizaciones aplicables a su infraestructura y versión se descargan y habilitan, y se ponen a disposición de su jerarquía. Esta sincronización puede ser automática o manual, según cómo configure el punto de conexión de servicio para la jerarquía:

-   En **modo en línea**, el punto de conexión de servicio se conecta al servicio en la nube de Microsoft automáticamente y descarga las actualizaciones aplicables.  

     De manera predeterminada, Configuration Manager busca nuevas actualizaciones cada 24 horas. También puede comprobar las actualizaciones inmediatamente. Para ello, seleccione **Buscar actualizaciones** en el nodo **Administración** > **Actualizaciones y mantenimiento** de la consola de Configuration Manager. (Antes de la versión 1702, este nodo se encontraba en **Administración** > **Cloud Services**).

-   En el **modo sin conexión**, el punto de conexión de servicio no se conecta al servicio en la nube de Microsoft. Para descargar y luego importar las actualizaciones disponibles, [use la herramienta de conexión de servicio para System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Puede importar correcciones fuera de banda en la consola. Para ello, utilice la [herramienta de registro de actualizaciones](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Estas correcciones fuera de banda complementan las actualizaciones que obtendrá al sincronizar con el servicio de Microsoft Cloud.


Una vez que las actualizaciones se sincronizan, puede verlas en la consola de Configuration Manager. Para ello, vaya al nodo **Administración** > **Actualizaciones y mantenimiento**:  

-   Las actualizaciones no instaladas se muestran como **Disponible**.

-   Las actualizaciones instaladas se muestran como **Instalado**.  Solo se muestra la última actualización instalada. Puede seleccionar el botón **Historial** de la cinta de opciones para ver las actualizaciones instaladas anteriormente.



Antes de configurar el punto de conexión de servicio, es conveniente conocer y planear sus usos adicionales. Los usos siguientes pueden afectar al modo en que se configura este rol de sistema de sitio:  

-   El punto de conexión de servicio se usa para cargar la información de uso sobre su sitio. Esta información ayuda al servicio en la nube de Microsoft a identificar las actualizaciones que están disponibles para la versión actual de su infraestructura. Para obtener más información, vea [Diagnósticos y datos de uso para System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   El punto de conexión de servicio se usa para administrar dispositivos con Microsoft Intune y con la administración local de dispositivos móviles de Configuration Manager. Para obtener más información, vea [Administración híbrida de dispositivos móviles (MDM) con System Center Configuration Manager y Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Para entender mejor lo que ocurre cuando se descargan las actualizaciones, vea:  

-   [Diagrama de flujo: descargar actualizaciones para System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Diagrama de flujo: actualizar la replicación para System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Asignar permisos para ver y administrar actualizaciones y características
Para que un usuario vea las actualizaciones en la consola, debe tener asignado un rol de seguridad de administración basado en roles que incluya la clase de seguridad **Paquetes de actualización**. Esta clase concede acceso para ver y administrar las actualizaciones en la consola de Configuration Manager.    

**Acerca de la clase Paquetes de actualización:**  
De forma predeterminada, **Paquetes de actualización** (SMS_CM_Updatepackages) forma parte de los siguientes roles de seguridad integrados con los permisos de la lista:
 -  **Administrador total** con permisos **Modificar** y **Lectura** :
    -   Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Todo** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación, y habilitar características individuales después de instalar la actualización.
    - Un usuario con este rol de seguridad y acceso al ámbito de seguridad **Predeterminado** puede ver e instalar las actualizaciones. El usuario también puede habilitar características durante la instalación, y ver características después de instalar la actualización. pero no puede habilitar las características después de instalar la actualización.

- **Analista de solo lectura** con permisos **Lectura** :
  -  Un usuario con este rol de seguridad y acceso al ámbito **Predeterminado** puede ver actualizaciones pero no instalarlas. Este usuario también puede ver características después de la instalación de una actualización, pero no puede habilitarlas.

**Permisos necesarios para la actualización y el mantenimiento:**   
  - Use una cuenta que tenga asignado un rol de seguridad que incluya la clase **Paquetes de actualización** con los permisos **Modificar** y **Lectura** .
  - La cuenta debe tener asignado el ámbito **Predeterminado** .

**Permisos para solo ver las actualizaciones**:
  - Use una cuenta que se asigna un rol de seguridad que incluye la clase **Paquetes de actualización** solo con el permiso **Lectura** .
  - La cuenta debe tener asignado el ámbito **Predeterminado** .

**Permisos necesarios para habilitar características después de instalar las actualizaciones:**
  -  Use una cuenta que tenga asignado un rol de seguridad que incluya la clase **Paquetes de actualización** con los permisos **Modificar** y **Lectura** .
  -  La cuenta debe tener asignado el ámbito **Todos** .



##  <a name="bkmk_beforeinstall"></a> Antes de instalar una actualización en la consola  
 Revise los pasos siguientes antes de instalar una actualización desde la consola de Configuration Manager.  

###  <a name="bkmk_step1"></a> Paso 1: Revisar la lista de comprobación de actualización  
Revise la lista de comprobación de actualización aplicable para las acciones que deben realizarse antes de iniciar la actualización:

- Actualización a 1606: vea [Lista de comprobación para la instalación de la actualización 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Actualización a 1610 desde 1606: vea [Lista de comprobación para la instalación de la actualización 1610](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Actualización a 1702 desde 1606 o 1610: vea [Lista de comprobación para la instalación de la actualización 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Paso 2: Ejecutar el comprobador de requisitos previos antes de instalar una actualización  
Antes de instalar una actualización, puede ejecutar la comprobación de requisitos previos para la actualización. Si ejecuta la comprobación de requisitos previos antes de instalar una actualización:  

-   Los archivos de actualización se replican en otros sitios antes de instalar la actualización.  

-   La comprobación de requisitos previos se vuelve a ejecutar automáticamente cuando decida instalar la actualización.  

> [!NOTE]   
> Cuando inicie una comprobación de requisitos previos y, a continuación, vea el estado, la fase de **instalación** parecerá estar activa, pero la actualización no se estará instalando realmente. Para cumplir el requisito previo de ejecutar una comprobación, el proceso de actualización extrae el paquete de la biblioteca de contenido y lo pone en una carpeta de almacenamiento provisional en la que se puede acceder a las comprobaciones de requisito previo actuales.  El mismo proceso se ejecuta cuando instala una actualización. Por este motivo, la instalación aparece como "En curso". En la categoría de instalación solo se muestra el paso *Extraer paquete de actualización*.  

Más adelante, cuando instale la actualización, puede configurarla para omitir las advertencias de comprobación de requisitos previos.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Para ejecutar el Comprobador de requisitos previos antes de instalar una actualización  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Actualizaciones y mantenimiento**.   

2.  Haga clic con el botón derecho en el paquete de actualización para el que desea ejecutar la comprobación de requisitos previos.  

3.  Seleccione **Ejecutar comprobación de requisitos previos**.  

     Cuando se ejecuta la comprobación de requisitos previos, el contenido de la actualización se replica a los sitios secundarios.  Puede ver el archivo distmgr.log en el servidor de sitio para confirmar que el contenido se replica correctamente.  

4.  Para ver los resultados de la comprobación, en la consola de Configuration Manager, vaya a **Supervisión** > **Actualizaciones y estado de mantenimiento** y busque el estado de requisitos previos. También puede consultar el archivo ConfigMgrPrereq.log en el servidor de sitio para obtener más detalles.  



##  <a name="bkmk_install"></a> Instalación de actualizaciones en la consola  
 Cuando esté listo para instalar actualizaciones en la consola de Configuration Manager, comience con el sitio de nivel superior de la jerarquía. Se trata del sitio de administración central o de un sitio primario independiente.  

 Se recomienda que instale la actualización fuera del horario comercial habitual para cada sitio a fin de minimizar el efecto sobre las operaciones empresariales. El motivo es que la instalación de la actualización puede incluir acciones como la reinstalación de componentes de sitio y de roles del sistema de sitio.  

-   Los sitios primarios secundarios inician la instalación de la actualización automáticamente después de que el sitio de administración central haya terminado de instalarla. Este es el proceso recomendado y predeterminado. En cambio, puede usar [Ventanas de servicio para servidores de sitio](/sccm/core/servers/manage/service-windows) para controlar el momento en que un sitio primario instala actualizaciones.  

-   Actualice manualmente los sitios secundarios desde la consola de Configuration Manager después de que el sitio principal primario haya terminado de instalar la actualización. No se admite la actualización automática de los servidores de sitio secundario.  

-   Cuando se usa una consola de Configuration Manager después de actualizar el sitio, también se le pide que actualice la consola.  

-  Después de que el servidor de sitio completa correctamente la instalación de una actualización, actualiza automáticamente todos los roles de sistema de sitio aplicables.  La única salvedad para esto hace referencia a los puntos de distribución. Al instalar una actualización, los puntos de distribución no se vuelven a instalar y se desconectan para actualizarse al mismo tiempo. En su lugar, el servidor de sitio usa la configuración de distribución de contenido del sitio para distribuir la actualización a un subconjunto de puntos de distribución a la vez. El resultado es que solo algunos puntos de distribución se desconectan para instalar la actualización. Los puntos de distribución que todavía no han comenzado a actualizarse o que han completado la actualización permanecen en línea y pueden proporcionar contenido a los clientes.


###  <a name="bkmk_overview"></a> Información general sobre la instalación de actualizaciones en la consola  
**1. Cuando se inicia la instalación de la actualización**  
Aparecerá el asistente para actualizaciones que muestra una lista de las áreas de producto a las que se aplica la actualización.  

-   En la página **General** del asistente, puede configurar **Advertencias de requisitos previos**.  
      -   Los errores de requisitos previos siempre detienen la instalación de la actualización. Solucione los errores para poder reintentar la instalación de la actualización de manera satisfactoria. Consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry) para más información.  

    -   Las advertencias de requisitos previos también pueden detener la instalación de la actualización. Solucione las advertencias antes de reintentar la instalación de la actualización. Para obtener más información, consulte [Reintento de la instalación de una actualización con errores](#bkmk_retry).  
    -   La opción **Pase por alto las advertencias de las comprobaciones de requisitos previos e instale esta actualización aunque falten requisitos** establece una condición para la instalación de la actualización que omite las advertencias de requisitos previos. Esto permite continuar con la instalación de la actualización. Si no selecciona esta opción, la instalación de la actualización se detiene cuando se encuentra una advertencia. A menos que ya haya ejecutado la comprobación de requisitos previos y haya resuelto las advertencias de requisitos previos para un sitio, no se recomienda usar esta opción.  

      En las áreas de trabajo **Administración** y **Supervisión**, el nodo Actualizaciones y mantenimiento incluye un botón en la cinta de opciones denominado **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos). Este botón está disponible cuando se produce un error al completar la instalación de un paquete de actualización debido a las advertencias de comprobación de los requisitos previos. Por ejemplo, instale una actualización sin utilizar la opción para ignorar las advertencias de requisitos previos (desde el Asistente para actualizaciones). La instalación de actualización se detiene con un estado de advertencia de requisitos previos, pero sin errores. Más adelante puede elegir **Omitir advertencias de requisitos previos** en la cinta de opciones para desencadenar una continuación automática de esa instalación de actualizaciones que, entonces, omite las advertencias de requisitos previos. Cuando se usa esta opción, la instalación de la actualización continúa automáticamente después de unos minutos.



-   Si se aplica una actualización al cliente de Configuration Manager, se le ofrecerá la opción de probar la actualización de cliente con un conjunto limitado de clientes. Para obtener más información, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante la instalación de la actualización**  
Como parte de la instalación de la actualización, Configuration Manager:  

-   Vuelve a instalar los componentes afectados, como los roles de sistema de sitio o la consola de Configuration Manager.  

-   Administra las actualizaciones de los clientes en función de las selecciones realizadas para las comprobaciones piloto de clientes y para las [actualizaciones de cliente automáticas](https://technet.microsoft.com/library/mt627885.aspx).  

-   No tendrá que reiniciar los servidores de sistema de sitio como parte de la actualización a menos que .NET esté instalado como parte de un requisito previo para roles de sistema de sitio.  

> [!TIP]  
>  Cuando se instalan actualizaciones, Configuration Manager también actualiza la carpeta CD.Latest. Esta carpeta se usa durante la recuperación del sitio.  

**3. Supervisar el progreso de las actualizaciones mientras se instalan**  
Para supervisar el progreso, utilice lo siguiente:  

-   En la consola de Configuration Manager, vaya al nodo **Administración** > **Actualizaciones y mantenimiento**. En este nodo se muestra el estado de instalación de todos los paquetes de actualización.


-   En la consola de Configuration Manager: nodo **Supervisión** > **Información general** > **Actualizaciones y estado de mantenimiento**. En este nodo se muestra solamente el estado de instalación del paquete de actualización que se esté instalando actualmente.  

    La instalación del paquete de actualización se divide en las siguientes fases para facilitar la supervisión. Para cada fase hay detalles adicionales, incluido el archivo de registro para ver más información:  
    -   **Descargar** (esta fase se aplica únicamente al sitio de nivel superior en el que está instalado el sitio del punto de conexión de servicio).   

    -   **replicación**   

    -   **Comprobación de requisitos previos**   

    -   **Instalación**    

    -   **Después de la instalación** ([las tareas posteriores a la instalación](#post-installation-tasks) están disponibles a partir de la versión 1610).  

-   Puede ver el archivo **CMUpdate.log** en **&lt;ConfigMgr_Installation_Directory>\Logs**.  

**4. Cuando se completa la instalación de la actualización**  
Después de que se completa la primera actualización del sitio:  

-   Los sitios primarios secundarios instalan la actualización automáticamente. No es necesario hacer nada.  

-   Los sitios secundarios deben actualizarse manualmente desde la consola de Configuration Manager.
> [!TIP]
> Aunque la versión de un sitio secundario no se muestre en la consola, puede usar el SDK de Configuration Manager para confirmar la versión de un sitio. Consulte [SMS_Site Server WMI Class](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Hasta el momento en que todos los sitios de la jerarquía estén actualizados a la nueva versión, la jerarquía funciona en modo de versión mixta. Para obtener más información, consulte [Interoperabilidad entre diferentes versiones de System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Actualizar consolas de Configuration Manager**  
Una vez que un sitio de administración central o un sitio primario se actualizan, cada consola de Configuration Manager que se conecta a ese sitio también debe actualizarse. Se le pide que actualice una consola:  

-   Cuando abre la consola.  

-   Cuando se desplaza a un nuevo nodo en una consola abierta.  

Se recomienda que instale la actualización inmediatamente.  

Cuando se complete la actualización de la consola, puede comprobar que la versión de la consola y del sitio es correcta. Vaya a **Acerca de System Center Configuration Manager** en la esquina superior izquierda de la consola.  

###  <a name="bkmk_toptier"></a> Para iniciar la instalación de la actualización en el sitio de nivel superior  
En el sitio de nivel superior de la jerarquía, en la consola de Configuration Manager, vaya a **Administración** > **Actualizaciones y mantenimiento**, seleccione una actualización **Disponible** y luego haga clic en **Instalar el paquete de actualización**.  

###  <a name="bkmk_secondary"></a> Para iniciar la instalación de la actualización en un sitio secundario  
Una vez que el sitio primario principal de un sitio secundario se actualiza, puede actualizar el sitio secundario desde la consola de Configuration Manager.  Para ello, utilice el **Asistente para actualizar sitios secundarios**.  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** > **Sitios**, seleccione el sitio que quiere actualizar y, luego, en la pestaña Inicio, en el grupo **Sitio**, haga clic en **Actualizar**.  

2.  Haga clic en **Sí** para iniciar la actualización del sitio secundario.  

Para supervisar la instalación de la actualización en un sitio secundario, seleccione el servidor de sitio secundario. Después, en la pestaña **Inicio**, en el grupo **Sitio**, seleccione **Mostrar estado de instalación**. También puede agregar la columna **Versión** a la consola para que pueda ver la versión de cada sitio secundario.  

Después de que un sitio secundario se actualice correctamente, si el estado de la consola no se actualiza o sugiere que la actualización ha producido errores, use la opción **Reintentar instalación**. Esta opción no vuelve a instalar la actualización del sitio secundario que instaló correctamente la actualización, sino que hace que la consola actualice el estado.

### <a name="post-installation-tasks"></a>Tareas posteriores a la instalación
A partir de la versión 1610, puede ver información acerca de las tareas posteriores a la instalación.

Cuando un sitio instala una actualización, hay varias tareas que no se pueden iniciar hasta que la actualización finalice la instalación en el servidor de sitio. Aquí mostramos una lista de las tareas posteriores a la instalación que son críticas para las operaciones de sitio y jerarquía. Dado que son críticas, se supervisan activamente. Entre las tareas adicionales que no se supervisan directamente se encuentra la reinstalación de los roles de sistema de sitio. Para ver el estado de la tareas de postinstalación críticas, seleccione la tarea **Postinstalación** durante la supervisión de la instalación de actualizaciones para un sitio.

No todas las tareas se completan de inmediato. Algunas tareas no se inician hasta que cada sitio complete la instalación de la actualización. Por lo tanto, la nueva funcionalidad que cabría esperar puede retrasarse hasta que se completen estas tareas. Por ejemplo, dado que la activación de nuevas características no se inicia hasta que todos los sitios completen la instalación de actualizaciones, es posible que las nuevas características no estén visibles durante algún tiempo.

Entre las tareas posteriores a la instalación figuran las siguientes:

-   **Instalación del servicio SMS_EXECUTIVE**
  -   Servicio crítico que se ejecuta en el servidor de sitio.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Subproceso de componente de sitio crítico del servicio SMS_EXECUTIVE.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_HIERARCHY_MANAGER**
  -   Componente de sitio crítico que se ejecuta en el servidor de sitio.
  -   Responsable de la reinstalación de los roles de sistema de sitio en los servidores de sistema de sitio.  El estado de la reinstalación del rol del sistema de sitio individual no se muestra.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente de sitio crítico que se ejecuta en el servidor de sitio.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Instalación del componente SMS_POLICY_PROVIDER**
  -   Componente de sitio crítico que se ejecuta solo en sitios primarios.
  -   La reinstalación de este servicio se debe completar rápidamente.


-   **Supervisando inicialización de replicación**   
  -   Esto se muestra solo en el sitio de administración central y los sitios primarios secundarios.
  -   Depende de SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Debe completarse rápidamente.


-   **Actualizando el paquete de preproducción del cliente de Configuration Manager**    
  -   Esto se muestra incluso cuando la preproducción del cliente (también llamada piloto de cliente) no está habilitada para su uso.
  -   No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.


-   **Actualizando la carpeta Client en el servidor de sitio**
  -   No se muestra si utiliza el cliente en preproducción.  
  -   Debe completarse rápidamente.


-   **Actualizando el paquete del cliente de Configuration Manager**
  -   No se muestra si utiliza el cliente en preproducción.  
  -   Finaliza solo después de que todos los sitios instalan la actualización.  


-   **Activación de características**
  -   Esto se muestra únicamente en el sitio de nivel superior de la jerarquía.
  -   No se inicia hasta que todos los sitios de la jerarquía terminan de instalar la actualización.
  -   No se muestran las características individuales.


##  <a name="bkmk_retry"></a> Reintento de la instalación de una actualización con errores  
Si no se puede instalar una actualización, revise los comentarios en la consola para identificar las soluciones de errores y las advertencias. También puede consultar el archivo ConfigMgrPrereq.log en el servidor de sitio para obtener más detalles. Antes de reintentar la instalación de una actualización, debe solucionar los errores y las advertencias.  

> [!TIP]  
> Si una actualización tiene problemas para descargar o replicar, puede usar la [herramienta de restablecimiento de actualizaciones](/sccm/core/servers/manage/update-reset-tool). Esta herramienta está disponible en los sitios que ejecutan la versión 1706 o posterior.

Cuando esté listo para volver a intentar la instalación de una actualización, seleccione la actualización con errores y elija una opción adecuada. El comportamiento del reintento de instalación de la actualización depende del nodo desde el que se inicia el reintento y de la opción de reintento que se usa.  

1.  **Vuelva a intentar la instalación en la jerarquía:**  
Puede volver a intentar la instalación de una actualización en toda la jerarquía si la actualización presenta alguno de los estados siguientes:  

    -   La comprobación de requisitos previos se ha superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualización de **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos) en el nodo **Actualizaciones y mantenimiento** es **No**).   
    -   Errores en la comprobación de requisitos previos    
    -   Error de instalación
    -   Error en la replicación del contenido en el sitio   

    Vaya a **Administración** > **Actualizaciones y mantenimiento**, seleccione la actualización y, después, elija una de las siguientes opciones:  

    -   **Reintentar**: al ejecutar **Reintentar** desde este nodo, la instalación de la actualización vuelve a empezar y omite automáticamente las advertencias de requisitos previos. También se vuelve a replicar el contenido para la actualización si no se pudo realizar la replicación previamente.
    - **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos): a partir de la versión 1606, si se detiene la instalación de la actualización debido a una advertencia, puede seleccionar **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos). Esta acción reinicia la instalación de la actualización y utiliza la opción para ignorar las advertencias de requisitos previos.   

2.  **Vuelva a intentar la instalación en el sitio:**  
 Puede volver a intentar la instalación de una actualización en un sitio específico si la actualización presenta alguno de los estados siguientes:  

    -   La comprobación de requisitos previos se ha superado con una o más advertencias y la opción de omitir las advertencias de comprobación de requisitos previos no se ha establecido en el Asistente para actualización. (El valor de actualización de **Ignorar advertencia sobre requisitos previos** en el nodo Actualizaciones y mantenimiento es **No**).  
    -   Errores en la comprobación de requisitos previos    
    -   Error de instalación    

    Vaya a **Supervisión** > **Introducción** > **Site Servicing Status**(Estado de mantenimiento del sitio), seleccione la actualización y haga clic en uno de los siguientes:

       - **Reintentar**: al ejecutar **Reintentar** desde este nodo, se reinicia la instalación de la actualización solo en ese sitio. A diferencia de ejecutar **Reintentar** en el nodo **Actualizaciones y mantenimiento**, este reintento no omite las advertencias de requisitos previos.
       -    **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos): a partir de la versión 1606, si se detiene la instalación de la actualización debido a una advertencia, puede hacer clic en **Ignore prerequisite warnings** (Omitir advertencias de requisitos previos). Esta acción reinicia la instalación de la actualización y utiliza la opción para ignorar las advertencias de requisitos previos.

##  <a name="bkmk_after"></a> Después de que un sitio instala una actualización  
Use la siguiente lista de comprobación para completar tareas comunes y configuraciones que se realizan después de actualizar un sitio.   

**Confirme que la replicación de sitio a sitio está activa:** en la consola de Configuration Manager, vaya a las siguientes ubicaciones para ver el estado y asegurarse de que la replicación está activa:  

-   **Supervisión** > **Introducción** > **Jerarquía del sitio**  

-   **Supervisión** > **Introducción** > **Replicación de base de datos**  

Para obtener más información, consulte [Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) y [Acerca de Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Confirme que los servidores de sitio y los servidores del sistema de sitio remoto se han reiniciado (si es necesario):** revise la infraestructura de sitio y asegúrese de que los servidores de sitio y los servidores de sistema de sitio aplicables se han reiniciado correctamente. Normalmente, los servidores de sitio se reinician solo si Configuration Manager instala .NET como un requisito previo para un rol de sistema de sitio.  

 **Actualice consolas independientes de Configuration Manager:** asegúrese de que todas las consolas remotas de Configuration Manager se actualizan a la misma versión. Se le pide que actualice una consola:  

-   Cuando se desplaza a un nuevo nodo en la consola.  

-   Cuando abre la consola.

**Vuelva a configurar réplicas de base de datos para puntos de administración en sitios primarios:** si utiliza réplicas de base de datos para puntos de administración en sitios primarios, debe desinstalar las réplicas de base de datos antes de actualizar el sitio. Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración. Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Vuelva a configurar todas las tareas de mantenimiento de base de datos deshabilitadas antes de la actualización:** si ha deshabilitado las [tareas de mantenimiento](../../../core/servers/manage/maintenance-tasks.md) de la base de datos en un sitio antes de instalar la actualización, vuelva a configurar esas tareas en el sitio. Use la misma configuración que había antes de la actualización.  

[Actualizar clientes:](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) para obtener más información, consulte **Actualizar clientes de equipos Windows con System Center Configuration Manager**.  

**Configuraciones adicionales:** revise los cambios realizados antes de iniciar la actualización y restaure esas configuraciones a sus sitios y jerarquías.  

##  <a name="bkmk_options"></a> Habilitar características opcionales de las actualizaciones  
Cuando una actualización incluye una o varias características opcionales, tiene la oportunidad de habilitar esas características en la jerarquía.  Puede habilitar características en el momento en que se instala la actualización, o bien volver a la consola en un momento posterior y habilitar las características opcionales.

Para ver las características disponibles y su estado, en la consola, vaya a **Administración** > **Actualizaciones y mantenimiento** > **Características**.

Cuando una característica no es opcional, se instala automáticamente y no aparece en el nodo **Características**.  


Al habilitar una característica nueva o de versión preliminar, el Administrador de jerarquía de Configuration Manager (HMAN) debe procesar el cambio antes de que dicha característica esté disponible. Generalmente el procesamiento del cambio es inmediato, pero puede tardar hasta 30 minutos en completarse, en función del ciclo de procesamiento de HMAN. Una vez que se haya procesado el cambio, debe reiniciar la consola para poder ver la nueva interfaz de usuario relacionada con esa característica.


##  <a name="bkmk_prerelease"></a> Uso de las características de versión preliminar de las actualizaciones
Las características de versión preliminar se incluyen en la Rama actual para realizar las primeras pruebas en un entorno de producción. Puede utilizar esas características en su entorno de producción, pero no se considera que estén listas para la producción. Obtenga más información sobre las [características de versión preliminar](/sccm/core/servers/manage/pre-release-features), incluida la manera de habilitarlas en el entorno.             


## <a name="known-issues"></a>Problemas conocidos

###  <a name="bkmk_faq"></a> ¿Por qué no se ven determinadas características en la consola?  
 Si no encuentra una actualización específica en la consola después de una sincronización correcta con el servicio en la nube de Microsoft, esto podría deberse a que:  

-   La actualización requiere una configuración que no utiliza la infraestructura o la versión de producto actual no cumple un requisito previo para recibir la actualización.  

     Si cree que tiene las configuraciones necesarias y otros requisitos previos para una actualización que falta, confirme que su punto de conexión de servicio se encuentra en modo en línea. Después, use la opción **Buscar actualizaciones** en el nodo **Actualizaciones y mantenimiento** para forzar una comprobación.  Si está establecido el modo sin conexión, debe usar la herramienta de conexión de servicio para realizar manualmente la sincronización con el servicio en la nube.  

-   La cuenta no dispone de los permisos de administración basada en roles correctos para ver las actualizaciones en la consola de Configuration Manager.

    Consulte [Permisos para administrar actualizaciones](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) en este tema para obtener información sobre los permisos necesarios para ver las actualizaciones y habilitar las características desde la consola.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>¿Por qué veo dos actualizaciones para la versión 1610?
Al ver las actualizaciones en la consola, es posible que vea dos actualizaciones para instalar la versión 1610. Estas actualizaciones tienen fechas distintas. Aparecen ambas cuando se cumple una de las condiciones siguientes:   
-   Ha instalado una versión anterior (por ejemplo, 1606) después de que estuviera disponible la versión 1610.

-   En su jerarquía se ejecuta la versión 1511 o 1602 y no ha podido descargar la versión 1606.

Hay dos versiones de actualización para la versión 1610, ya que esta actualización se ha vuelto a publicar después de realizar algunos cambios secundarios en archivos binarios. Estos cambios no afectan al funcionamiento de Configuration Manager ni a la actualización.

Si las dos actualizaciones están disponibles en la consola, le recomendamos que instale la actualización con la fecha más reciente. En cambio, como las dos actualizaciones ofrecen las mismas funciones, si ya ha instalado una de ellas, no es necesario que realice otra acción.
-   Si anteriormente ha instalado la actualización anterior, no es necesario que instale la actualización con la fecha más reciente. Sin embargo, si instala la actualización más reciente después de instalar la primera actualización, se actualizarán los archivos binarios en cuestión. No se produce ningún cambio adicional y no se necesita ninguna otra acción por parte del usuario.

-   Si ha instalado anteriormente la versión más reciente y, después, instala la actualización con la fecha anterior, no es necesario que realice ninguna otra acción. Esto se debe a que los archivos binarios más recientes que ya ha instalado no se sobrescriben con los mismos binarios de la actualización original.
