---
title: Supervisión de la replicación
titleSuffix: Configuration Manager
description: Aprenda a supervisar la infraestructura y las operaciones en Configuration Manager mediante el área de trabajo Supervisión de la consola.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04faf92545f84fdf53c522ad9aa0c74bbd5c4aa1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342280"
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Supervisar la infraestructura de la jerarquía y replicación de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Para supervisar la infraestructura y las operaciones de System Center Configuration Manager, use el área de trabajo **Supervisión** en la consola de Configuration Manager.  

> [!NOTE]  
>  La excepción a esta ubicación es Migración, que se supervisa directamente en el nodo **Migración** del área de trabajo **Administración** . Para obtener más información, vea [Operaciones para migrar a System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 Además de utilizar la consola de Configuration Manager para la supervisión, puede utilizar los informes de Configuration Manager, o ver los archivos de registro de Configuration Manager para los componentes de Configuration Manager. Para más información sobre los informes, consulte [Generación de informes en System Center Configuration Manager](../../../core/servers/manage/reporting.md). Para más información sobre los archivos de registro, consulte [Archivos de registro en System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Al supervisar los sitios, busque signos que indiquen problemas que requiera que realice una acción. Por ejemplo:  

-   Un trabajo pendiente de archivos en servidores de sitios y sistemas de sitio.  

-   Mensajes de estado que indican un error o un problema.  

-   Error en la comunicación dentro de un sitio.  

-   Mensajes de error y de advertencia en el registro de eventos del sistema en servidores.  

-   Mensajes de error y de advertencia en el registro de errores de Microsoft SQL Server.  

-   Sitios o clientes que no informan desde hace tiempo.  

-   Respuesta lenta de la base de datos de SQL Server.  

-   Indicios de errores de hardware.  

Para minimizar el riesgo de un error del sitio, si las tareas de supervisión revelan indicios de problemas, investigue el origen del problema y repárelo lo antes posible.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Supervisar tareas de administración comunes para Configuration Manager  
 Configuration Manager proporciona supervisión integrada desde la propia consola de Configuration Manager. Puede supervisar muchas tareas, entre otras, las relacionadas con actualizaciones de software, administración de energía e implementación de contenido en toda la jerarquía.  

 Use la información siguiente para obtener ayuda en la supervisión de tareas comunes de Configuration Manager:  

 **Alertas**  
   Vea [Supervisar alertas](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) en [Usar alertas y el sistema de estado de System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Configuración de conformidad**  
   Consulte [Cómo supervisar la configuración de cumplimiento en System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Implementación de contenido**  
   Para más información sobre la supervisión de contenido, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Para obtener información acerca de la supervisión de los tipos específicos de implementación de contenido:
-   Para más información sobre la supervisión de aplicaciones, consulte [Supervisar aplicaciones con System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Para supervisar paquetes y programas, consulte Cómo administrar paquetes y programas en [Paquetes y programas en System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Consulte [Cómo supervisar Endpoint Protection en System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Supervisión de administración de energía**  
 Consulte [Cómo supervisar y planear la administración de energía en System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Supervisión de disponibilidad de software**  
Consulte [Supervisar el uso de aplicaciones a través de la medición de software en System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Supervisar actualizaciones de software**  
 Consulte [Monitor software updates in System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md) (Supervisión de actualizaciones de software en System Center Configuration Manager).  


##  <a name="BKMK_MonitorInfrastructure"></a> Supervisar la infraestructura de la jerarquía para Configuration Manager  
Configuration Manager proporciona varios métodos para supervisar el estado y las operaciones de la jerarquía. Puede comprobar el estado del sistema de sitios de toda la jerarquía, supervisar la replicación entre sitios desde una visualización jerárquica o geográfica, supervisar los vínculos de replicación entre sitios para la replicación de bases de datos y usar la herramienta Replication Link Analyzer para solucionar problemas de replicación.  

###  <a name="BKMK_SH_Node"></a> Acerca del nodo Jerarquía de sitio  
El nodo **Jerarquía del sitio** del área de trabajo **Supervisión** proporciona una visión general de la jerarquía de Configuration Manager y de los vínculos entre sitios. Puede utilizar dos vistas:  

-   **Diagrama de jerarquía**: esta vista muestra la jerarquía como un mapa topológico simplificado para mostrar solamente la información esencial.  

-   **Vista geográfica**: esta vista presenta los sitios en un mapa geográfico que muestra las ubicaciones de sitios que configure.  

Use el nodo **Jerarquía del sitio** para supervisar el estado de cada sitio y los vínculos de replicación entre sitios y su relación con factores externos, como una ubicación geográfica.  

Dado que el estado del sitio y el estado del vínculo entre sitios se replican como datos de sitio y no como datos globales, cuando conecte la consola de Configuration Manager a un sitio primario secundario, no podrá ver el estado del sitio ni del vínculo para otros sitios primarios ni para sus sitios secundarios. Por ejemplo, en una jerarquía de sitios primarios múltiples, si la consola de Configuration Manager se conecta a un sitio primario, podrá ver el estado de los sitios secundarios, del sitio primario y del sitio de administración central, pero no podrá ver el estado para otros nodos de la jerarquía que pertenezcan al sitio de administración central.  

 Use el comando **Configurar valores** para controlar cómo se representa la visualización de la jerarquía de sitios. Las configuraciones realizadas en el nodo **Jerarquía de sitios** cuando se conecte la consola de Configuration Manager a un sitio se replican al resto de sitios.  

#### <a name="hierarchy-diagram"></a>Diagrama de jerarquía  
 El diagrama de jerarquía muestra los sitios en un mapa de topología. En esta vista, puede seleccionar un sitio y ver un resumen de mensajes de estado de dicho sitio, explorar en profundidad para ver mensajes de estado y acceder al cuadro de diálogo **Propiedades** de los sitios.  

 Además, puede pausar el puntero del mouse en un vínculo de sitio o de replicación entre sitios para ver el estado de alto nivel para ese objeto. Dado que el estado del vínculo de replicación no se replica globalmente, en una jerarquía con varios sitios primarios, deberá conectar la consola de Configuration Manager al sitio de administración central para ver los detalles del vínculo de replicación entre todos los sitios.  

 Las siguientes opciones modifican el diagrama de jerarquía:  

-   **Grupos**: puede configurar el número de sitios primarios y secundarios que desencadenan un cambio en la visualización del diagrama de jerarquía que combina los sitios en un solo objeto. Cuando los sitios se combinan en un único objeto, verá el número total de sitios y un resumen de alto nivel de mensajes de estado y estado de sitio. Las configuraciones de grupo no afectan a la vista geográfica.  

-   **Sitios favoritos**: puede especificar los sitios como sitios favoritos. Un icono de estrella identifica un sitio favorito en el diagrama de jerarquía. Los sitios favoritos no se combinan con otros sitios si utilizó grupos, y siempre se muestran de forma individual.  

#### <a name="geographical-view"></a>Vista geográfica  
 La vista geográfica muestra la ubicación de cada sitio en un mapa geográfico. Solo se mostrarán los sitios que configure con una ubicación. Cuando seleccione un sitio en esta vista, se mostrarán los vínculos de replicación a sitios primarios o secundarios. A diferencia de la vista Diagrama de jerarquía, en esta vista no puede mostrar mensajes de estado del sitio ni detalles del vínculo de replicación.  

> [!NOTE]  
>  Para usar la vista geográfica, el equipo al que se conecte la consola de Configuration Manager deberá tener instalado Internet Explorer y poder acceder a Mapas de Bing mediante el protocolo HTTP.  

La siguiente opción modifica la vista geográfica.  

-   **Ubicación del sitio**: puede especificar una ubicación geográfica para cada sitio. Puede especificar la ubicación como una dirección postal, el nombre de un lugar tal como el nombre de una ciudad, o mediante las coordenadas de latitud y longitud. Por ejemplo, para usar la latitud y longitud de Redmond (Washington, EE.UU.), debería especificar **N 47 40 26.3572 O 122 7 17.4432** como ubicación del sitio. No es necesario especificar los símbolos de grado, minutos o segundos de longitud o latitud. Configuration Manager usa Mapas de Bing para mostrar la ubicación en la vista geográfica. Esto le proporciona la opción de ver la jerarquía con relación a una ubicación geográfica, lo que puede proporcionar información sobre problemas locales que pudieran afectar a determinados sitios o a la replicación entre sitios.  

     Cuando se especifica una ubicación, puede utilizar el cuadro **Ubicación** para buscar un sitio específico en la jerarquía. Con el sitio seleccionado, introduzca la ubicación como nombre de la ciudad o dirección postal en la columna **Ubicación** . Configuration Manager utiliza Mapas de Bing para resolver la ubicación.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Cómo supervisar los vínculos de replicación de bases de datos y el estado de replicación  
 Además de los detalles de alto nivel que son accesibles desde el nodo **Jerarquía del sitio** en el área de trabajo **Supervisión** . También puede supervisar los detalles para la replicación de base de datos cuando use el nodo **Replicación de base de datos** en el área de trabajo **Supervisión** . Desde **Replicación de base de datos**, podrá supervisar el estado de los vínculos de replicación entre sitios y los detalles de inicialización y de replicación para los grupos de replicaciones en el sitio al que esté conectada la consola de Configuration Manager.  

> [!TIP]  
>  Aunque también aparece un nodo **Replicación de base de datos** debajo del nodo **Configuración de jerarquía** en el área de trabajo **Administración** , desde esta ubicación no podrá ver el estado de replicación para los vínculos de replicación de bases de datos.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Estado de vínculo de replicación  
La replicación de bases de datos entre sitios implica la replicación de varios conjuntos de información, denominados grupos de replicación. Cada grupo de replicación se replica con diferentes prioridades de replicación. De forma predeterminada, no se pueden modificar los datos contenidos en un grupo de replicación ni la frecuencia de replicación.  

 Cuando un vínculo de replicación está activo y no tiene el estado de error o degradado, todos los grupos de replicación se replican oportunamente. Si uno o varios grupos de replicación no completan la replicación dentro del período de tiempo esperado, el vínculo se muestra como degradado. Los vínculos degradados podrían funcionar aún, pero deberá supervisarlos para asegurarse de que vuelvan a su estado activo o investigarlos para comprobar si hay más errores de degradación o replicación.  

 Para cada vínculo de replicación puede especificar el número de veces que un grupo de replicación que no se replicó correctamente intenta replicarse de nuevo antes de que el estado del vínculo pase a degradado o error. Aunque se repliquen correctamente todos los grupos de replicación menos uno, el estado pasará a degradado o error, pues un grupo de replicación no pudo completar la replicación dentro del número de intentos especificado. Para más información sobre los umbrales de replicación, consulte la sección [Umbrales de replicación de base de datos](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) del tema [Transferencias de datos entre sitios en System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md) .  

 Utilice la información de la tabla siguiente para conocer el estado de los vínculos de replicación que podrían requerir más investigación.  

|Descripción del vínculo|Más información|  
|----------------------|----------------------|  
|**El vínculo está activo**|No se detectó ningún problema y la comunicación a través del vínculo es actual.|  
|**El vínculo está degradado**|La replicación es funcional, pero la replicación de al menos un objeto o grupo se retrasó. Supervise los vínculos que se encuentran en este estado, y revise la información de ambos sitios del vínculo para obtener indicaciones sobre el posible error del vínculo.<br /><br /> Un vínculo también puede mostrar el estado degradado si el sitio que recibe los datos replicados no puede confirmar rápidamente los datos en la base de datos. Esto puede suceder cuando se replican grandes volúmenes de datos. Por ejemplo, si implementa una actualización de software en un número elevado de equipos, el volumen de datos que se replica podría necesitar un cierto tiempo para su procesamiento por parte del sitio principal del vínculo. El retardo en el procesamiento del sitio principal podría hacer que el estado del vínculo se estableciera en degradado hasta que el sitio principal pueda procesar correctamente el trabajo pendiente de datos.|  
|**Se ha producido un error en el vínculo**|La replicación no es funcional. Es posible que un vínculo de replicación pueda recuperarse sin necesidad de otras acciones. Puede utilizar Replication Link Analyzer para investigar y corregir la replicación en este vínculo.<br /><br /> Este estado también puede indicar un problema con la red física entre el sitio principal y secundario en el vínculo de replicación.|  

 Cuando un sitio principal se encuentre en proceso de actualización a un nuevo Service Pack y vea el estado del vínculo desde el sitio secundario, el estado del vínculo se mostrará como activo. Después de la actualización, hasta que el sitio secundario se encuentre también en el mismo Service Pack que el principal, el estado del vínculo se mostrará como activo cuando se visualice desde el sitio principal, y como en configuración cuando se visualice desde el sitio secundario.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Estado de replicación  
 Puede usar el nodo **Replicación de base de datos** del área de trabajo **Supervisión** para ver el estado de replicación para un vínculo de replicación y ver información acerca de la base de datos del sitio en cada sitio del vínculo de replicación. También puede ver detalles sobre los grupos de replicación. Para ver detalles, seleccione un vínculo de replicación y, a continuación, seleccione la pestaña correspondiente al estado de replicación que desea ver. A continuación se proporcionan detalles acerca de las diferentes pestañas del estado de replicación.  

 **Resumen**  
 Muestra información de alto nivel acerca de la replicación de datos del sitio y datos globales entre los dos sitios de un vínculo.  

 También puede hacer clic en **Ver informes de datos de tráfico del historial** para ver un informe con detalles sobre el ancho de banda de red usado por la replicación en todo el vínculo de replicación.  

 **Sitio principal**  
 Para el sitio principal de un vínculo de replicación, muestra detalles acerca de la base de datos, que incluyen:  

-   Puertos de firewall para SQL Server  

-   Espacio libre en disco  

-   Ubicaciones de los archivos de base de datos  

-   Certificados  

**Sitio secundario**  
 Para el sitio secundario de un vínculo de replicación, muestra detalles acerca de la base de datos, que incluyen:  

-   Puertos de firewall para SQL Server  

-   Espacio libre en disco  

-   Ubicaciones de los archivos de base de datos  

-   Certificados  

**Detalle de inicialización**    
 Muestra el estado de inicialización para los grupos de replicación que se replican a través del vínculo de replicación. Esta información puede permitirle identificar cuándo la inicialización de datos de replicación está en curso o no terminó correctamente.  

 Además, puede utilizar esta información para identificar cuándo podría estar un sitio en modo de interoperabilidad. El modo de interoperabilidad se produce cuando el sitio secundario no ejecuta la misma versión de Configuration Manager que el sitio principal.  

**Detalle de la replicación**    
 Consulte el estado de replicación de cada grupo de replicación que se replica a través del vínculo. Consulte esta información para facilitar la identificación de problemas o retrasos en la replicación de datos específicos, y para ayudar a determinar los umbrales de replicación de base de datos apropiados para este vínculo. Para más información sobre los umbrales de replicación de base de datos, consulte la sección [Umbrales de replicación de base de datos](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) del tema [Transferencias de datos entre sitios en System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md) .  

> [!TIP]  
>  Los grupos de replicación de datos de sitio se envían sólo desde el sitio secundario al sitio principal. Los grupos de replicación de datos globales replican en ambas direcciones.  

###  <a name="BKMK_RLA"></a> Acerca de Replication Link Analyzer  
 Configuration Manager incluye **Replication Link Analyzer**, que se utiliza para analizar y reparar problemas de replicación. Puede utilizar Replication Link Analyzer para corregir errores del vínculo de replicación cuando hay errores de replicación y cuando la replicación deja de funcionar pero aún no se ha registrado el error. Se puede utilizar Replication Link Analyzer para remediar problemas de replicación entre los siguientes equipos de la jerarquía de Configuration Manager (no importa la dirección del error de replicación):  

-   Entre un servidor de sitio y el servidor de base de datos de sitio.  

-   Entre un servidor de base de datos de sitios y otro equipo de base de datos de sitios (replicación entre sitios).  

Puede ejecutar Replication Link Analyzer en la consola de Configuration Manager o en un símbolo del sistema:  

-   Para ejecutar la ejecución en la consola de Configuration Manager: en el área de trabajo **Supervisión**, haga clic en el nodo **Replicación de base de datos**, seleccione el vínculo de replicación que desea analizar y, a continuación, en el grupo **Replicación de base de datos** de la pestaña **Inicio**, seleccione **Replication Link Analyzer**.  

-   Para realizar la ejecución en un símbolo del sistema, escriba el siguiente comando: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;FQDN del servidor de sitio de origen\> &lt;FQDN del servidor de sitio de destino\>**  

Cuando se ejecuta Replication Link Analyzer, éste detecta los problemas con una serie de comprobaciones y reglas de diagnóstico. Cuando se ejecuta la herramienta, puede ver los problemas que identifica la herramienta. Se muestran las instrucciones conocidas para resolver un problema. Si Replication Link Analyzer puede corregir un problema automáticamente, se le ofrece dicha opción. Cuando Replication Link Analyzer finaliza, guarda los resultados en el siguiente informe basado en XML y un archivo de registro en el escritorio del usuario que ejecuta la herramienta:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Cuando se ejecuta Replication Link Analyzer, detiene los servicios siguientes mientras se corrigen algunos problemas, y reinicia dichos servicios después de solucionar el problema:  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

Si se produce algún error en Replication Link Analyzer para realizar la corrección, revise el servidor de sitio y reinicie los servicios si se han detenido.  

Las acciones de investigación y corrección que se realizan correcta e incorrectamente se registran para ofrecer detalles adicionales que no se muestran en la interfaz de la herramienta.  

**Requisitos previos para usar Replication Link Analyzer:**  

-   La cuenta que se utiliza para ejecutar Replication Link Analyzer debe tener derechos de administrador local en cada equipo al que remite el vínculo de replicación. La cuenta no requiere un rol específico de seguridad de administración basada en roles. Por tanto, un usuario administrativo con acceso al nodo **Replicación de base de datos** puede ejecutar la herramienta en la consola de Configuration Manager, o un administrador del sistema con derechos suficientes en cada equipo puede ejecutar la herramienta en un símbolo del sistema.  

-   La cuenta que se utiliza para ejecutar Replication Link Analyzer debe tener derechos de administrador del sistema en cada base de datos SQL Server a la que remite el vínculo de replicación.  

**Problemas conocidos de Replication Link Analyzer:**  

-   Con el lanzamiento de System Center Configuration Manager versión 1511, Replication Link Analyzer genera errores de certificado de SQL Server Service Broker para los sitios primarios que se actualizaron desde System Center 2012 Configuration Manager. Esto es debido a cambios en los nombres de los certificados introducidos con la versión 1511, para los que Replication Link Analyzer aún no se ha actualizado. Pueden omitirse estos errores de forma segura.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procedimientos para supervisar la replicación de base de datos  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>Para supervisar el estado de replicación de base de datos entre sitios de alto nivel    
1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Jerarquía del sitio** para abrir la vista **Diagrama de jerarquía** .  

3.  Coloque el puntero del mouse brevemente en la línea que divide los dos sitios para ver el estado de replicación global y de replicación de datos de sitio para estos sitios.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Para supervisar el estado de replicación para un vínculo de replicación    
1.  En la consola de Configuration Manager, haga clic en **Supervisión**.  

2.  En el área de trabajo **Supervisión** , haga clic en **Replicación de base de datos**y, a continuación, seleccione el vínculo de replicación que desea supervisar. A continuación, en el área de trabajo, seleccione la pestaña correspondiente para ver distintos detalles acerca del estado de replicación de ese vínculo.  
