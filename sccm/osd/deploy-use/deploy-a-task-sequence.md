---
title: Implementar una secuencia de tareas
titleSuffix: Configuration Manager
description: Utilice esta información para implementar una secuencia de tareas en los equipos de una colección.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c3aca04273c25326c64d696a44089b6c8d1222bf
ms.sourcegitcommit: 2ef7e69f3db54a90ed4ae2a3f59a75e6329a1584
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71062123"
---
# <a name="deploy-a-task-sequence"></a>Implementar una secuencia de tareas

Después de crear una secuencia de tareas y distribuir el contenido al que se hace referencia, impleméntela en una colección de dispositivos. Esta acción permite que la secuencia de tareas se ejecute en un dispositivo. Una secuencia de tareas implementada se puede ejecutar automáticamente, o cuando un usuario la instala en el dispositivo.

> [!WARNING]  
> Puede administrar el comportamiento de las implementaciones de secuencias de tareas de alto riesgo. Una implementación de alto riesgo es una implementación que se instala automáticamente y puede provocar resultados no deseados. Por ejemplo, una secuencia de tareas con el propósito **Requerido** que implementa un sistema operativo se considera una implementación de alto riesgo. Para obtener más información, consulte [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configuración para administrar implementaciones de alto riesgo).  


## <a name="process"></a>Proceso

Utilice el siguiente procedimiento para implementar una secuencia de tareas en los equipos de una recopilación.  

> [!NOTE]  
> Los mensajes de estado para la implementación de la secuencia de tareas se muestran en la ventana Mensaje en un sitio primario, pero no se muestran en un sitio de administración central.  

1. En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software**, expanda **Sistemas operativos** y, luego, seleccione el nodo **Secuencias de tareas**.  

2. En la lista **Secuencia de tareas** , seleccione la secuencia de tareas que desee implementar.  

3. En la pestaña **Inicio** de la cinta de opciones, vaya al grupo **Implementación** y seleccione **Implementar**.  

    > [!NOTE]  
    > Si **Implementar** no está disponible, la secuencia de tareas tiene una referencia que no es válida. Corrija la referencia y, a continuación, intente implementar la secuencia de tareas de nuevo.  

4. En la página **General**, especifique la siguiente información.  

    - **Secuencia de tareas**: especifique la secuencia de tareas para implementar. De forma predeterminada, este cuadro muestra la secuencia de tareas seleccionada.  

    - **Recopilación**: seleccione la recopilación que contiene los equipos que ejecutan la secuencia de tareas.  

        No implemente una secuencia de tareas que instale un sistema operativo en recopilaciones inapropiadas, como la recopilación de todos los servidores del centro de datos. Asegúrese de que la recopilación que seleccione contiene solo los equipos que desea que ejecuten la secuencia de tareas.  

        Para más información sobre implementaciones de alto riesgo, consulte [Implementaciones de alto riesgo](#bkmk_high-risk).

    - **Usar grupos de puntos de distribución predeterminados asociados a esta recopilación**: almacene el contenido de la secuencia de tareas en el grupo de puntos de distribución predeterminado de la recopilación. Si no ha asociado la colección seleccionada a un grupo de puntos de distribución, esta opción estará atenuada.  

    - **Distribuir contenido automáticamente para las dependencias**: si alguno de los contenidos a los que se hace referencia tiene dependencias, el sitio también enviará contenido dependiente a los puntos de distribución.  

    - **Descargar contenido previamente para esta secuencia de tareas**: para obtener más información, consulte [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/configure-precache-content).  

    - **Seleccionar plantilla de implementación**: a partir de la versión 1802 de Configuration Manager,<!--1357391--> puede guardar y especificar una plantilla de implementación para una secuencia de tareas.  

        > [!IMPORTANT]  
        > En Configuration Manager versión 1802, algunos elementos no se guardan en la plantilla.  <!--510610--> Asegúrese de que estos elementos se aplican al ejecutar el asistente para la implementación:  
        >
        > - Instalación de software
        > - Programación
        > - Descarga previa de contenido

    - **Comentarios (opcional)** : especifique información adicional que describa esta implementación de la secuencia de tareas.  

5. En la página **Configuración de implementación**, especifique la siguiente información:  

    - **Propósito**: en la lista desplegable, elija una de las opciones que se indican a continuación.  

        - **Disponible**: el usuario ve la secuencia de tareas en el Centro de software y la puede instalar a petición.  

        - **Obligatoria**: Configuration Manager ejecuta la secuencia de tareas automáticamente de acuerdo con la programación configurada. Si la secuencia de tareas no está oculta, el usuario todavía puede seguir su estado de implementación. También puede usar el Centro de software para instalar la secuencia de tareas antes de la fecha límite.  

        > [!NOTE]
        > Si varios usuarios inician sesión en el dispositivo, es posible que las implementaciones de paquete y secuencia de tareas no aparezcan en el centro de Software.  

    - **Estar disponible para**: especifique si la secuencia de tareas está disponible para uno de los tipos siguientes:  

        - Solo clientes de Configuration Manager  
        - Clientes de Configuration Manager, medios y PXE  
        - Solo medios y PXE  
        - Sólo medios y PXE (ocultos)  

        > [!IMPORTANT]  
        > Use la opción **Sólo medios y PXE (ocultos)** para implementaciones automatizadas de secuencia de tareas. Para que el equipo arranque automáticamente en la implementación sin interacción del usuario, seleccione **Permitir la implementación desatendida de sistema operativo** y configure la variable **SMSTSPreferredAdvertID** como parte del medio. Para obtener más información sobre las variables de secuencia de tareas para esta acción, consulte [Task sequence variables](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID) (Variables de secuencia de tareas).  

    - **Enviar paquetes de reactivación**: si la implementación es **Obligatoria** y selecciona esta opción, el sitio envía un paquete de reactivación a los equipos antes de que el cliente ejecute la implementación. Este paquete reactiva el equipo en suspensión a la hora límite de instalación. Para poder usar esta opción, los equipos y las redes deben configurarse para Wake On LAN. Para obtener más información, vea [Planear la reactivación de clientes](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

    - **Permitir a los clientes de una conexión a Internet de uso medido descargar contenido una vez cumplida la fecha límite de instalación, lo cual podría suponer costes adicionales**: esta opción solo está disponible para implementaciones de tipo **Obligatoria**. Si tiene una secuencia de tareas personalizada que instala una aplicación pero no implementa un sistema operativo, puede especificar si permite a los clientes descargar contenido una vez cumplida la fecha límite de la instalación cuando utilizan una conexión a Internet de uso medido. En ocasiones, los proveedores de acceso a Internet cobran según la cantidad de datos que use cuando se utiliza una conexión de uso medido.  

        > [!NOTE]  
        > Aunque el uso de una conexión a Internet de uso medido podría funcionar para secuencias de tareas que no implementan un sistema operativo, no se admite este tipo de conexión para este propósito.  

6. En la página **Programación**, especifique la siguiente información:  

    > [!IMPORTANT]  
    > Cuando un cliente de Windows PE se inicia desde PXE o desde un medio de arranque, el cliente no evalúa las programaciones de implementación. Estas programaciones incluyen las horas límite, de inicio y de expiración. Configure programaciones en implementaciones únicamente en clientes que se inicien desde el sistema operativo Windows completo. Considere el uso de otros métodos (como periodos de mantenimiento) para controlar las secuencias de tareas activas implementadas en clientes que se inician desde Windows PE.  

    - **Programar cuándo estará disponible esta implementación**: especifique la fecha y hora en que la secuencia de tareas estará disponible para ejecutarse en el equipo de destino. Cuando seleccione la opción **UTC**, la secuencia de tareas estará disponible para varios equipos al mismo tiempo. En caso contrario, la implementación estará disponible en horas diferentes, según la hora local en cada equipo.  

        Si la hora de inicio es anterior a la hora requerida, el cliente descarga el contenido de la secuencia de tareas a la hora de inicio.  

    - **Programar cuándo expirará esta implementación**: especifique la fecha y hora en que expirará la secuencia de tareas en el equipo de destino. Cuando seleccione la opción **UTC**, la secuencia de tareas expirará en varios equipos de destino al mismo tiempo. En caso contrario, la implementación expira en horas diferentes, según la hora local en cada equipo.  

    - **Programación de asignación**: para una implementación **Obligatoria**, especifique cuándo ejecuta el cliente la secuencia de tareas. Puede agregar varias programaciones. La programación de asignación puede tener una de las siguientes configuraciones:  

        - Una fecha y hora específicas  
        - Patrón de periodicidad mensual, semanal o personalizado  
        - En cuanto sea posible  
        - Eventos de inicio o cierre de sesión  

        > [!NOTE]  
        > Si programa una hora de inicio para una implementación obligatoria que sea anterior a la fecha y hora en que la secuencia de tareas está disponible, el cliente de Configuration Manager descarga el contenido a la hora de inicio asignada. Este comportamiento se produce incluso si ha programado la secuencia de tareas para que esté disponible en un momento posterior.<!--SCCMDocs issue 777-->  

    - **Comportamiento de reejecución**: especifique cuándo se vuelve a ejecutar la secuencia de tareas. Seleccione una de las siguientes opciones:  

        - **Nunca volver a ejecutar el programa implementado**: si el cliente ya ha ejecutado la secuencia de tareas, no se vuelve a ejecutar. La secuencia de tareas no se vuelve a ejecutar, aunque no se completara en su primera ejecución o los archivos hayan cambiado.  

        - **Volver a ejecutar siempre el programa**: la secuencia de tareas siempre se vuelve a ejecutar en el cliente cuando se programa la implementación. Se vuelve a ejecutar incluso si la secuencia de tareas ya se ha ejecutado correctamente. Esta opción es útil cuando se usan implementaciones periódicas en las que la secuencia de tareas se actualiza regularmente.  

            > [!IMPORTANT]  
            > Esta opción está seleccionada de forma predeterminada. Sin embargo, no surte ningún efecto hasta que se asigne una implementación obligatoria. Un usuario siempre puede volver a ejecutar las implementaciones disponibles.  

        - **Volver a ejecutar en caso de error del intento anterior**: la secuencia de tareas se vuelve a ejecutar cuando se programa la implementación, solo si anteriormente no se pudo ejecutar. Esta opción es útil para las implementaciones obligatorias. Si el último intento de ejecución no se completó correctamente, las implementaciones reintentarán automáticamente su ejecución de acuerdo a la programación de asignación.  

        - **Volver a ejecutar si el intento anterior se realizó correctamente**: la secuencia de tareas se vuelve a ejecutar solo si se ejecutó antes correctamente en el cliente. Esta configuración es útil cuando se utiliza en implementaciones periódicas en las que la secuencia de tareas se actualiza periódicamente, y cada actualización requiere que la actualización anterior está instalada correctamente.  

        > [!NOTE]  
        > Un usuario puede volver a ejecutar una implementación de secuencia de tareas disponible. Antes de implementar una secuencia de tareas disponible en un entorno de producción, pruebe en primer lugar qué sucede si un usuario vuelve a ejecutar la secuencia de tareas varias veces.  

7. En la página **Experiencia del usuario** , especifique la siguiente información:  

    - **Permitir que los usuarios ejecuten el programa independientemente de las asignaciones**: especifique si un usuario puede ejecutar una implementación obligatoria fuera de la programación de asignación. Esta opción siempre está habilitada para las implementaciones disponibles.  

    - **Mostrar progreso de la secuencia de tareas**: especifique si el cliente de Configuration Manager debe mostrar el progreso de la secuencia de tareas.  

    - **Instalación de software**: especifique si el usuario puede instalar software fuera de la ventana de mantenimiento configurada después del tiempo programado.  

    - **Reinicio del sistema (si es necesario para completar la instalación)** : especifique si se permite al usuario reiniciar el equipo tras una instalación de software fuera de una ventana de mantenimiento configurada tras la hora de asignación.  

    - **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: esta configuración controla el comportamiento de instalación en dispositivos Windows Embedded habilitados con un filtro de escritura. Elija esta opción para que los cambios se confirmen en la fecha límite de instalación o durante una ventana de mantenimiento. Al seleccionar esta opción, se necesita un reinicio y los cambios persisten en el dispositivo. De lo contrario, la aplicación se instala en la superposición temporal y se confirma más tarde. Cuando implemente una secuencia de tareas en un dispositivo de Windows Embedded, asegúrese de que el dispositivo es miembro de una recopilación que tenga una ventana de mantenimiento configurada.  

    - **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**: especifique si se permite que la secuencia de tareas se ejecute en un cliente basado en Internet. Las operaciones que requieren un medio de arranque, como la instalación de un sistema operativo, no se admiten con esta configuración. Use esta opción solo para instalaciones de software genéricas o secuencias de tareas basadas en scripts que realizan operaciones en el sistema operativo estándar.  

        - A partir de la versión 1802, esta configuración se admite para implementaciones de una secuencia de tareas de actualización local de Windows 10 en clientes basados en Internet a través de Cloud Management Gateway. Para obtener más información, vea [Implementar una actualización local de Windows 10 a través de CMG](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. En la página **Alertas**, especifique la configuración de alertas de esta implementación de secuencia de tareas.  

9. En la página **Puntos de distribución** , especifique la siguiente información:  

    - **Opciones de implementación**: especifique una de las siguientes opciones.  

        > [!NOTE]  
        > Si usa multidifusión para implementar un sistema operativo, descargue el contenido cuando se necesite o antes de que se ejecute la secuencia de tareas.  

        - **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas**: especifica que los clientes descargan el contenido desde el punto de distribución según sea necesario mediante la secuencia de tareas. El cliente inicia la secuencia de tareas. Cuando un paso de una secuencia de tareas requiera contenido, este se descarga antes de que se ejecute el paso.  

        - **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas**: especifica que los clientes descargan todo el contenido desde el punto de distribución antes de que se ejecute la secuencia de tareas. Si ha hecho que la secuencia de tareas esté disponible para implementaciones del medio de arranque y PXE en la página **Configuración de implementación**, esta opción no se muestra.  

        - **Acceder al contenido directamente desde un punto de distribución cuando sea necesario mediante la ejecución de la secuencia de tareas**: especifica que los clientes ejecutan el contenido del punto de distribución. Esta opción está disponible solo cuando todos los paquetes asociados con la secuencia de tareas están habilitados para utilizar un recurso compartido de paquete en el punto de distribución. Para habilitar el contenido de tal modo que utilice un recurso compartido de paquete, consulte la pestaña **Acceso a datos** en las **Propiedades** de cada paquete.  

            > [!IMPORTANT]  
            > Para mayor seguridad, seleccione las opciones **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** o **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas**. Cuando se selecciona cualquiera de estas opciones, Configuration Manager aplica un algoritmo hash al paquete, por lo que se puede garantizar la integridad del paquete. Cuando se selecciona la opción **Acceder al contenido directamente desde un punto de distribución cuando sea necesario mediante la ejecución de la secuencia de tareas**, Configuration Manager no comprueba el hash del paquete antes de ejecutar el programa especificado. Dado que el sitio no puede garantizar la integridad del paquete, es posible que los usuarios con derechos administrativos alteren o manipulen el contenido del paquete.  

    - **Cuando no haya disponible ningún punto de distribución local, usar un punto de distribución remoto**: especifica si los clientes pueden usar puntos de distribución de grupos de límite vecino para descargar el contenido necesario para la secuencia de tareas.  

    - **Permitir que los clientes usen puntos de distribución del grupo de límite del sitio predeterminado**: especifica si los clientes deben descargar contenido desde un punto de distribución en el grupo de límites predeterminados del sitio, cuando el contenido no está disponible desde un punto de distribución en el grupo actual o en los grupos de límites vecinos.  

        > [!Note]  
        > A partir de la versión 1810, cuando un dispositivo ejecuta una secuencia de tareas y necesita adquirir contenido, usa los comportamientos de grupos de límites similares al cliente de Configuration Manager. Para obtener más información, vea [Task sequence support for boundary groups](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd) (Compatibilidad de la secuencia de tareas con grupos de límites).<!--1359025-->  

10. A partir de Configuration Manager 1802, en la pestaña **Resumen**, seleccione **Guardar como plantilla** si quiere guardar la configuración para usarla de nuevo. Asigne un nombre a la plantilla y seleccione la configuración que quiere guardar.  

11. Complete el asistente.  


## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Implementar una actualización local de Windows 10 a través de CMG

<!-- 1357149 -->
A partir de la versión 1802, la secuencia de tareas de actualización local de Windows 10 admite la implementación en los clientes basados en Internet que se administran a través de [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG). Esta función permite a los usuarios remotos actualizar con mayor facilidad a Windows 10 sin necesidad de conectarse a la intranet.

Asegúrese de que todo el contenido al que hace referencia la secuencia de tareas de actualización en contexto se distribuye a un [punto de distribución de nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). En caso contrario, los dispositivos no podrán ejecutar la secuencia de tareas.

Cuando se implementa una secuencia de tareas de actualización, utilice la siguiente configuración:

- **Permitir que la secuencia de tareas se ejecute para el cliente en Internet**, en la pestaña Experiencia del usuario de la implementación.  

- **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas** en la página Puntos de distribución de la implementación. Otras opciones como **Descargar el contenido localmente cuando sea necesario mediante la ejecución de una secuencia de tareas** no funcionan en este escenario. El motor de la secuencia de tareas no puede obtener contenido actualmente desde un punto de distribución de nube. El cliente de Configuration Manager debe descargar el contenido desde el punto de distribución de nube antes de iniciar la secuencia de tareas.  

- (*Opcional*) **Descargar contenido previamente para esta secuencia de tareas** en la pestaña General de la implementación. Para obtener más información, vea [Configuración del contenido de la caché previa](/sccm/osd/deploy-use/configure-precache-content).  


## <a name="bkmk_high-risk"></a> Administración de implementaciones de alto riesgo

Al realizar una implementación de alto riesgo, como un sistema operativo, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones personalizadas que cumplen con la configuración de comprobación de implementación que está configurada en las propiedades del sitio. Las implementaciones de alto riesgo siempre se limitan a las recopilaciones personalizadas, las recopilaciones que cree y la recopilación integrada **Equipos desconocidos** . Si crea una implementación de alto riesgo, no podrá seleccionar una recopilación integrada como **Todos los sistemas**. Para ver todas las recopilaciones personalizadas que contienen menos clientes que el tamaño máximo configurado, desactive **Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio**. Para obtener más información, consulte [Settings to manage high-risk deployments](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) (Configuración para administrar implementaciones de alto riesgo).  

La configuración de comprobación de implementación se basa en la pertenencia actual de la recopilación. Después de implementar la secuencia de tareas, Configuration Manager no vuelve a evaluar la pertenencia a la recopilación para la configuración de implementación de alto riesgo.  

Por ejemplo, supongamos que establece el **Tamaño predeterminado** en 100 y el **Tamaño máximo** en 1000. Al crear una implementación de alto riesgo, en la ventana **Seleccionar recopilación** solo se muestran las recopilaciones que contienen menos de 100 clientes. Si desactiva la opción **Hide collections with a member count greater than the site's minimum size configuration** (Ocultar recopilaciones con un número de miembros superior a la configuración de tamaño mínimo del sitio), en la ventana se muestran las recopilaciones que contienen menos de 1000 clientes.  

Al seleccionar una recopilación que contiene un rol de sitio, se aplica el comportamiento siguiente:  

- Si la recopilación contiene un servidor de sistema de sitio y ha configurado los valores de comprobación de implementación de modo que bloqueen las recopilaciones con servidores de sistema de sitio, se producirá un error. No podrá seguir creando la implementación.  

- Si se aplica uno de los siguientes criterios, el Asistente para implementar software muestra una advertencia de alto riesgo. Para continuar, debe aceptar que se cree una implementación de alto riesgo. El sitio genera un mensaje de estado de auditoría.  

    - Si la recopilación contiene un servidor de sistema de sitio y ha configurado los valores de comprobación de implementación de modo que adviertan sobre las recopilaciones con servidores de sistema de sitio  

    - Si la recopilación supera el valor de tamaño predeterminado

    - Si la recopilación contiene un servidor  


## <a name="see-also"></a>Consulte también

[Administrar secuencias de tareas para automatizar tareas](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)
