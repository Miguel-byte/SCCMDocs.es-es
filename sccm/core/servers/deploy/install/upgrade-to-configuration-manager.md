---
title: Actualizar a System Center Configuration Manager | Microsoft Docs
description: "Obtenga información sobre qué pasos seguir para ejecutar correctamente una actualización local desde un sitio y jerarquía que ejecutan System Center 2012 Configuration Manager."
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 90775fcf2549080a43e9c1606caa79d9eb90a89c
ms.openlocfilehash: 057cd079e452321a51c41797e8dd1a8f5b6a5688
ms.contentlocale: es-es
ms.lasthandoff: 05/02/2017


---
# <a name="upgrade-to-system-center-configuration-manager"></a>Actualizar a System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Puede ejecutar una actualización local para actualizar a System Center Configuration Manager desde un sitio y jerarquía que ejecutan System Center 2012 Configuration Manager.  

 Antes de actualizar desde System Center 2012 Configuration Manager, debe preparar los sitios, lo que requiere quitar configuraciones específicas que pueden impedir la correcta actualización, y luego seguir la secuencia de actualización si existe más de un sitio implicado.  

 > [!TIP]
 > Al administrar el sitio de System Center Configuration Manager y la infraestructura de la jerarquía, los términos *actualizar* ** e *instalar* se usan para describir tres conceptos independientes. Para obtener información sobre cómo se usa cada término, vea [Acerca de la actualización e instalación](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Rutas de actualización local  

**Actualizar a la versión 1702**   
Si tiene el medio de línea base de la versión 1702, puede actualizar lo siguiente a una versión con licencia completa de System Center Configuration Manager versión 1702:   
-      Una instalación de evaluación de System Center Configuration Manager versión 1702
-      Una instalación de versión candidata para lanzamiento de System Center Configuration Manager
-      System Center 2012 Configuration Manager con Service Pack 1
-      System Center 2012 Configuration Manager con Service Pack 2
-      System Center 2012 R2 Configuration Manager
-      System Center 2012 R2 Configuration Manager con Service Pack 1

**Actualizar a la versión 1606**  
El 15 de diciembre de 2016, se volvió a publicar el medio de línea base para la versión 1606 a fin de agregar compatibilidad con más escenarios de actualización. Esta nueva versión admite la actualización de lo siguiente a una versión con licencia completa de System Center Configuration Manager versión 1606:  
-   Una instalación de evaluación de System Center Configuration Manager versión 1606
-   Una instalación de versión candidata de System Center Configuration Manager  
-   System Center 2012 Configuration Manager con Service Pack 1  
-   System Center 2012 Configuration Manager con Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager con Service Pack 1  

Si usa un medio de línea base de la versión 1606 descargado antes del 15 de diciembre de 2016, solo puede actualizar lo siguiente a una versión con licencia completa de System Center Configuration Manager versión 1606:
-   Una instalación de evaluación de System Center Configuration Manager versión 1606
-   System Center 2012 Configuration Manager con Service Pack 2
-   System Center 2012 R2 Configuration Manager con Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  Al realizar la actualización desde una versión de System Center 2012 Configuration Manager a la Rama actual, es posible simplificar el proceso de actualización. Para obtener más información, consulte:  
>   
>  -   La sección [Versiones de línea base y versiones de actualización](../../../../core/servers/manage/updates.md#bkmk_Baselines) de [Actualizaciones para System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [La carpeta CD.Latest para System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **No se admite lo siguiente:**  
-   No se admite la actualización de Technical Preview para System Center Configuration Manager a una instalación con licencia completa.  Una versión de Technical Preview solo puede actualizarse a una versión posterior de Technical Preview.  

-   No se admite la migración desde una versión de Technical Preview a una versión con licencia completa.  

##  <a name="bkmk_checklist"></a> Lista de comprobación de actualización  
 Las listas de comprobación siguientes pueden ayudarle a planear una actualización correcta a System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Antes de realizar la actualización  

**Revise el entorno de System Center 2012 Configuration Manager** y resuelva problemas como se detalla en KB4018655: [Configuration Manager clients reinstall every five hours because of a recurring retry task and may cause an inadvertent client upgrade](https://support.microsoft.com/help/4018655) (Los clientes de Configuration Manager se reinstalan cada cinco horas debido a una tarea periódica de reintento, lo que puede provocar una actualización de cliente involuntaria).

**Asegurarse de que el entorno informático cumple las configuraciones admitidas** requeridas para la actualización a System Center Configuration Manager:  

Revise los sistemas operativos de servidor en uso para hospedar roles de sistema de sitio:  

-   Algunos sistemas operativos anteriores que System Center 2012 Configuration Manager admitía no se admiten en System Center Configuration Manager, y los roles de sistema de sitio en estos sistemas operativos deben reubicarse o quitarse antes de la actualización. Consulte la documentación de [Sistemas operativos compatibles con servidores de sistema de sitio de System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).   
-   El comprobador de requisitos previos para Configuration Manager no comprueba los requisitos previos para roles de sistema de sitio en el servidor de sitio ni en los sistemas de sitio remotos  

Revise los requisitos previos requeridos para cada equipo que hospeda un rol de sistema de sitio:  

-   Por ejemplo, System Center Configuration Manager usa Windows 10 Assessment and Deployment Kit (Windows ADK) para implementar un sistema operativo. Antes de ejecutar el programa de instalación, debe descargar e instalar Windows 10 ADK en el servidor del sitio y en cada uno de los equipos que ejecutan una instancia del proveedor de SMS.  

Para obtener información general sobre las plataformas admitidas y las configuraciones de los requisitos previos, consulte [Configuraciones admitidas para System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Para obtener más información sobre el uso de Windows ADK con Configuration Manager, consulte [Requisitos de infraestructura para la implementación de sistema operativo en System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Revise el estado del sitio y de la jerarquía y compruebe que no hay problemas sin resolver:**  
Antes de actualizar un sitio, resuelva todos los problemas de funcionamiento para el servidor del sitio, el servidor de base de datos del sitio y los roles del sistema de sitio instalados en los equipos remotos. La actualización del sitio puede generar errores debido a problemas de funcionamiento existentes.  

**Instale todas las actualizaciones críticas aplicables de los sistemas operativos en los equipos que hospedan el sitio, el servidor de base de datos del sitio y los roles del sistema de sitio remoto:**  
Antes de actualizar un sitio, instale las actualizaciones críticas para cada sistema de sitio aplicable. Si alguna de las actualizaciones que instala requiere un reinicio, reinicie los equipos correspondientes antes de iniciar la actualización del Service Pack.  

Para obtener más información, consulte [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Desinstale los roles de sistema de sitio no compatibles con System Center Configuration Manager:**  
Los siguientes roles de sistema de sitio ya no se usan en System Center Configuration Manager y deben desinstalarse antes de actualizar desde System Center 2012 Configuration Manager:  

-   Punto de administración fuera de banda  
-   Punto de validador de mantenimiento del sistema  

**Deshabilite las réplicas de la base de datos para los puntos de administración en los sitios primarios:**  
Configuration Manager no puede actualizar correctamente un sitio primario que tiene habilitada una réplica de base de datos para puntos de administración. Deshabilite la replicación de base de datos antes de:  

-   Crear una copia de seguridad de la base de datos del sitio para probar la actualización de la base de datos.  
-   Actualizar el sitio de producción a System Center Configuration Manager  

Para obtener más información, consulte:  
-   System Center 2012 Configuration Manager: [Configurar réplicas de bases de datos para puntos de administración](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Vuelva a configurar los puntos de actualización de software que usan NLB:**  
Configuration Manager no puede actualizar un sitio que usa un clúster de equilibrio de carga de red (NLB) para hospedar puntos de actualización de software.  

Si utiliza clústeres NLB para puntos de actualización de software, use PowerShell para quitar el clúster NLB. (A partir de System Center 2012 Configuration Manager SP1, no hay ninguna opción en la consola de Configuration Manager para configurar un clúster NLB)  

**Deshabilite todas las tareas de mantenimiento del sitio en cada sitio mientras dure la actualización del sitio:**  
Antes de actualizar a System Center Configuration Manager, deshabilite cualquier tarea de mantenimiento del sitio que pueda estar en ejecución mientras el proceso de actualización esté activo. Esto incluye, entre otras cosas, lo siguiente:  

-   Copia de seguridad del servidor del sitio  
-   Eliminar operaciones cliente antiguas  
-   Eliminar datos de detección antiguos  

Cuando se ejecuta una tarea de mantenimiento de base de datos durante el proceso de actualización, se puede producir un error en la actualización del sitio.  

Antes de deshabilitar una tarea, programe la tarea de forma que pueda restaurar su configuración después de finalizar la actualización del sitio.  

Para obtener más información acerca de las tareas de mantenimiento del sitio, consulte:  

-   System Center 2012 Configuration Manager: [Planeación de las tareas de mantenimiento de Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager: [Referencia de tareas de mantenimiento para System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Ejecutar el comprobador de requisitos previos del programa de instalación.**:  
Antes de actualizar un sitio, puede ejecutar el **comprobador de requisitos previos** independientemente del programa de instalación para comprobar que el sitio cumple los requisitos previos. Después, cuando actualiza el sitio, el comprobador de requisitos previos se ejecuta otra vez.  

Si usa el medio de línea base para la versión 1606 de la versión de octubre de 2016, la comprobación de requisitos previos independiente evalúa el sitio para la actualización a la Rama actual y a la Rama de mantenimiento a largo plazo (LTSB) de System Center Configuration Manager. Dado que LTSB no admite algunas características, podría ver entradas en *ConfigMgrPrereq.log* parecidas a las siguientes:
 - INFO: The site is a LTSB edition. (INFORMACIÓN: El sitio es una edición LTSB.)
 - Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. (Rol de sistema de sitio "Punto de sincronización de Asset Intelligence" no admitido para la edición LTSB; Error; Configuration Manager ha detectado que está instalado el "Punto de sincronización de Asset Intelligence".) Asset Intelligence no se admite en la edición LTSB. Debe desinstalar el rol de sistema de sitio del punto de sincronización de Asset Intelligence para poder continuar.

Si tiene previsto actualizar a la Rama actual, puede pasar por alto sin problema los errores relacionados con la edición LTSB. Solo se aplican si tiene previsto actualizar a LTSB.

Después, cuando ejecute el programa de instalación de Configuration Manager para realizar la actualización, se llevará a cabo de nuevo la comprobación de requisitos previos para evaluar el sitio según la rama de System Center Configuration Manager que decida instalar (Rama actual o LTSB). Si decide actualizar a la Rama actual, no se llevará a cabo la comprobación de características que no son compatibles con LTSB.

Para obtener más información, consulte [Comprobador de requisitos previos](/sccm/core/servers/deploy/install/prerequisite-checker) y [Lista de comprobaciones previas de System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Descargue los archivos de requisitos previos y los archivos redistribuibles para System Center Configuration Manager:**    
Use el **descargador del programa de instalación** para descargar los archivos redistribuibles de requisitos previos, los paquetes de idioma y las actualizaciones más recientes del producto para System Center Configuration Manager.  

Para obtener información, consulte [Descargador del programa de instalación](/sccm/core/servers/deploy/install/setup-downloader).  

**Planear la administración de los idiomas de los servidores y los clientes**:  
Cuando se actualiza un sitio, la actualización del sitio instala solo las versiones del paquete de idioma que se seleccionan durante la actualización.  

-   El programa de instalación revisa la configuración de idioma actual del sitio y, a continuación, identifica los paquetes de idioma disponibles en la carpeta donde se almacenan los archivos de requisitos previos descargados previamente.  
-   Puede confirmar la selección actual de paquetes de idioma de servidores y clientes, o cambiar las selecciones para agregar o quitar compatibilidad para determinados idiomas.  
-   Solo se pueden seleccionar los paquetes de idioma que están disponibles al ejecutar el programa de instalación (que se obtienen con los archivos de requisitos previos descargados).  

> [!NOTE]  
>  No puede usar paquetes de idioma de System Center 2012 Configuration Manager para habilitar idiomas para un sitio de System Center Configuration Manager.  

Para obtener más información sobre los paquetes de idioma, consulte [Paquetes de idioma en System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Revisar las consideraciones para las actualizaciones de sitio**:  
Al actualizar un sitio, algunas características y configuraciones restablecen su configuración predeterminada. Para ayudarle a prepararse para estos cambios y otros relacionados, revise la información de  [Consideraciones sobre la actualización](#bkmk_considerations).  

**Cree una copia de seguridad de la base de datos del sitio en el sitio de administración central y los sitios primarios:**  
Antes de actualizar un sitio, haga una copia de seguridad de la base de datos del sitio para asegurarse de que dispone de una copia de seguridad preparada para una recuperación ante desastres.  

Consulte [Copia de seguridad y recuperación de System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Realizar una copia de seguridad de un archivo Configuration.mof personalizado**:  
Si utiliza un archivo Configuration.mof personalizado para definir clases de datos que se utilizan con el inventario de hardware, cree una copia de seguridad de este archivo antes de actualizar el sitio. Tras la actualización, restaure este archivo al sitio. Para obtener más información sobre el uso de este archivo, consulte [Cómo ampliar el inventario de hardware en System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Pruebe el proceso de actualización de la base de datos en una copia de la última copia de seguridad de la base de datos del sitio:**  
Antes de actualizar un sitio primario o un sitio de administración central de Configuration Manager, pruebe la el proceso de actualización de la base de datos del sitio en una copia de la base de datos del sitio.  

-   Debe probar el proceso de actualización de base de datos del sitio porque, al actualizar un sitio, la base de datos del sitio podría modificarse.  
-   Aunque una actualización de base de datos de prueba no es necesaria, puede identificar problemas de la actualización antes de que la base de datos de producción se vea afectada.  
-   Una actualización incorrecta de la base de datos del sitio podría inutilizar la base de datos del sitio, en cuyo caso podría ser necesaria una recuperación del sitio para restaurar la funcionalidad.  
-   Aunque se trate de una base de datos de sitio compartida entre varios sitios de una jerarquía, planee la prueba de la base de datos en cada uno de los sitios correspondientes antes de actualizar el sitio.  
-   Si usa réplicas de base de datos para puntos de administración en un sitio primario, deshabilite la replicación antes de crear la copia de seguridad de la base de datos del sitio.  

Configuration Manager no admite la realización de copias de seguridad de sitios secundarios ni la actualización de prueba de una base de datos de un sitio secundario.  

No se puede ejecutar una actualización de prueba de base de datos en la base de datos del sitio de producción. Esta acción actualiza la base de datos del sitio y podría inutilizar el sitio.  

Para obtener más información, vea [Probar la actualización de la base de datos del sitio](#bkmk_test).  

**Reinicie el servidor de sitio y todos los equipos que hospeden un rol de sistema de sitio**:  
Debe hacerlo para asegurase de que no haya acciones pendientes de una instalación reciente de actualizaciones o de requisitos previos. Se trata de un proceso interno específico de la compañía.  

**Actualizar sitios**:  
En el sitio de primer nivel de la jerarquía, ejecute Setup.exe desde los medios de origen de System Center Configuration Manager.  

Después de que se actualice el sitio de primer nivel puede comenzar la actualización de los sitios secundarios. No comience la actualización de un sitio hasta que finalice la anterior.  

Hasta el momento en que todos los sitios de la jerarquía estén actualizados a System Center Configuration Manager, la jerarquía funciona en modo de versión mixta.  

Para obtener información sobre cómo ejecutar la actualización, consulte [Actualizar sitios](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Después de realizar la actualización  
**Actualice las consolas independientes de Configuration Manager**:  
De manera predeterminada, cuando actualiza un sitio de administración central o un sitio primario, la consola de Configuration Manager instalada en el servidor de sitio también se actualiza. Sin embargo, debe actualizar manualmente cada una de las consolas que esté instalada en un equipo distinto del servidor de sitio.  

> [!TIP]  
>  Cierre todas las consolas abiertas antes de iniciar la actualización.  

Para obtener más información, consulte [Instalar las consolas de System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).  

**Vuelva a configurar réplicas de base de datos para los puntos de administración de los sitios primarios:**  
Si utiliza réplicas de base de datos para puntos de administración en sitios primarios, debe desinstalar las réplicas de base de datos antes de actualizar el sitio. Después de actualizar un sitio primario, vuelva a configurar la réplica de base de datos de los puntos de administración.   
Para obtener más información, consulte [Réplicas de bases de datos para puntos de administración de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Vuelva a configurar todas las tareas de mantenimiento de la base de datos que haya deshabilitado antes de la actualización:**  
Si ha deshabilitado la [referencia de tareas de mantenimiento para System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) de una base de datos en un sitio antes de la actualización, vuelva a configurar dichas tareas en el sitio con la misma configuración que había antes de la actualización.  

**Actualizar clientes.**:  
Después de actualizar todos los sitios a System Center Configuration Manager, planifique la actualización de los clientes.  

Cuando se actualiza un cliente, se desinstala el software cliente actual y se instala la nueva versión de software cliente. Para actualizar clientes, puede usar cualquier método admitido por Configuration Manager.  

> [!TIP]  
>  Al actualizar el sitio de primer nivel de una jerarquía, también se actualiza el paquete de instalación de cliente en cada punto de distribución de la jerarquía. Cuando se actualiza un sitio primario, se actualiza el paquete de actualización de cliente que está disponible en ese sitio primario.  

Para obtener más información sobre cómo actualizar clientes existentes y cómo instalar nuevos clientes, consulte [Actualizar clientes de equipos Windows con System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Consideraciones sobre la actualización  
**Acciones automáticas**:  
Cuando se realiza la actualización a System Center Configuration Manager, se producen de forma automática las siguientes acciones:  

-   El sitio realiza un restablecimiento de sitio que incluye una reinstalación de todos los roles de sistema de sitio.  
-   Si el sitio es el sitio de nivel superior de una jerarquía, actualiza el paquete de instalación de cliente en cada punto de distribución en la jerarquía. El sitio también actualiza las imágenes de arranque predeterminadas para que usen la nueva versión de Windows PE incluida en el Windows Assessment and Deployment Kit 10. Sin embargo, la actualización no actualiza el medio existente para su uso con la implementación de la imagen.  
-   Si el sitio es un sitio primario, actualiza el paquete de actualización de cliente para ese sitio.  

**Acciones manuales del usuario administrativo después de una actualización**   
Después de actualizar un sitio, asegúrese de que se llevan a cabo las siguientes acciones:  

-   Asegúrese de que los clientes asignados a cada sitio primario realizan la actualización e instalación del software cliente de la nueva versión.  
-   Actualice cada consola de Configuration Manager que se conecta al sitio y que se ejecuta en un equipo remoto con respecto al servidor de sitio.  
-   En los sitios primarios en los que usa réplicas de base de datos para puntos de administración, vuelva a configurar las réplicas de base de datos.  
-   Después de actualizar el sitio, deberá actualizar manualmente los medios físicos, como los como archivos ISO de CDs y DVDs o las unidades flash USB, o los medios preconfigurados que se han usado para las implementaciones de Windows To Go o que se han proporcionado a los proveedores de hardware. Aunque la actualización del sitio actualiza las imágenes de arranque predeterminadas, no puede actualizar estos dispositivos o archivos multimedia externos a Configuration Manager  
-   Tenga previsto actualizar las imágenes de arranque no predeterminadas cuando no necesite la versión original (antigua) de Windows PE.  

**Acciones que afectan a las opciones y configuraciones**   
Cuando un sitio se actualiza a System Center Configuration Manager, algunas opciones y configuraciones no se conservan después de la actualización o se establecen nuevas configuraciones predeterminadas. En la tabla siguiente se incluyen las configuraciones que no se conservan o que cambian, y se proporciona información detallada para ayudarlo a planearlas durante la actualización del sitio:  

-   **Centro de software:**  
    Se restablecen los valores predeterminados de los siguientes elementos del Centro de software:  
    -   **Información del trabajo** : se restablece un horario comercial de **5:00 a.m.** a **10:00 p.m.** , de lunes a viernes.  
    -   El valor de **Mantenimiento del equipo** se configura como **Suspender las actividades del Centro de software si el equipo está en modo Presentación**.  
    -   El valor de **Control remoto** se configura según el valor en la configuración de cliente asignada al equipo.  
-   **Programaciones de resumen de actualización de software:**  
     Las programaciones de resumen personalizadas para actualizaciones de software o grupos de actualizaciones de software se restablecen al valor predeterminado de 1 hora. Al finalizar la actualización, restablezca los valores personalizados de resumen según la frecuencia necesaria.  

##  <a name="bkmk_test"></a> Probar la actualización de la base de datos del sitio  
La siguiente información solo se aplica cuando se actualiza una versión anterior como System Center 2012 Configuration Manager a System Center Configuration Manager. Si el sitio ya ejecuta System Center Configuration Manager y va a instalar una actualización nueva, consulte [Paso 2: Probar la actualización de la base de datos antes de instalar una actualización](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) en **Antes de instalar una actualización en la consola**.

Antes de actualizar un sitio, pruebe una copia de la base de datos de ese sitio para la actualización.  

Para probar la base de datos para una actualización, primero debe restaurar una copia de la base de datos del sitio a una instancia de SQL Server que no hospede un sitio de Configuration Manager. La versión de SQL Server que use para hospedar la copia de la base de datos debe ser una versión de SQL Server compatible con la versión de Configuration Manager que sea el origen de la copia de la base de datos.  

Después, tras restaurar la base de datos del sitio, en el equipo con SQL Server, ejecute el programa de instalación de Configuration Manager desde la carpeta de medios de origen de System Center Configuration Manager con la opción de línea de comandos **/TESTDBUPGRADE**.  

-   Para obtener información sobre cómo crear y restaurar una copia de seguridad de una base de datos del sitio, consulte [Opciones de línea de comandos para el programa de instalación](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para obtener información sobre la opción de línea de comandos **/TESTDBUPGRADE**, consulte la tabla que aparece en [Opciones de línea de comandos para el programa de instalación](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Para más información sobre las versiones compatibles de SQL Server, consulte el tema [Compatibilidad con versiones de SQL Server para System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Si integra Microsoft Intune con Configuration Manager:  
>   
>  al ejecutar una actualización de base de datos de prueba en la copia de la base de datos del sitio de 5 o más días de antigüedad, es posible que reciba un mensaje similar a los siguientes:  
>   
>  -   ADVERTENCIA: La actualización forzará la sincronización completa en la nube.  
>  -   ERROR: La actualización de la base de datos forzará la sincronización completa en la nube.  
>   
> Ambos pueden omitirse de manera segura durante las pruebas de una actualización de base de datos, ya que no indican un error o un problema con la actualización de prueba. En su lugar, indican que, durante la actualización real, los datos del grupo de replicación de base de datos en la **nube** pueden sincronizarse con Microsoft Intune.  

Utilice el siguiente procedimiento en cada sitio de administración central y el sitio primario que tiene previsto actualizar.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Para probar una base de datos de sitio para la actualización  

1.  Realice una copia de la base de datos del sitio y luego restaure dicha copia en una instancia de SQL Server que use la misma edición que la base de datos de su sitio y que no hospede un sitio de Configuration Manager. Por ejemplo, si la base de datos del sitio se ejecuta en una instancia de la edición Enterprise de SQL Server, asegúrese de que restaure la base de datos a una instancia de SQL Server que también ejecute la edición Enterprise.  

2.  Tras restaurar la copia de la base de datos, ejecute el programa de instalación desde los medios de origen de System Center Configuration Manager. Cuando ejecute el programa de instalación, use la opción de línea de comandos **/TESTDBUPGRADE** . Si la instancia de SQL Server que hospeda la copia de la base de datos no es la instancia predeterminada, también deberá indicar los argumentos de la línea de comandos para identificar la instancia que hospeda la copia de la base de datos del sitio.  

     Por ejemplo, tiene previsto actualizar una base de datos de sitio con el nombre SMS_ABC. Restaura una copia de esta base de datos del sitio a una instancia compatible de SQL Server con el nombre de instancia DBTest. Para probar una actualización de esta copia de la base de datos del sitio, use la siguiente línea de comandos: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Puede encontrar Setup.exe en la siguiente ubicación del medio de origen de System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  En la instancia de SQL Server donde se ejecuta la actualización de la base de datos de prueba, supervise el archivo ConfigMgrSetup.log en la raíz de la unidad del sistema para ver el progreso y el éxito:  

    -   Si se produce un error en la prueba de actualización, resuelva cualquier problema relacionado con la actualización de la base de datos del sitio, cree una nueva copia de seguridad de la base de datos del sitio y, a continuación, pruebe la actualización de la nueva copia de la base de datos.  
    -   Una vez completado el proceso correctamente, puede eliminar la copia de la base de datos.  

        > [!NOTE]  
        >  No se puede restaurar la copia de la base de datos del sitio que se utiliza para la actualización de prueba para su uso como una base de datos de sitio en cualquier sitio.  

Después de actualizar una copia de la base de datos del sitio correctamente, continúe con la actualización del sitio de Configuration Manager y su base de datos del sitio.  

##  <a name="bkmk_upgrade"></a> Actualizar sitios  
Tras completar las configuraciones previas a la actualización de su sitio, probar la actualización de la base de datos del sitio en una copia de la base de datos y descargar archivos de requisitos previos y paquetes de idioma para la versión de Service Pack que planee instalar, estará listo para actualizar su sitio de Configuration Manager.  

Cuando se actualiza un sitio en una jerarquía, primero debe actualizar el sitio de nivel superior de la jerarquía. Este sitio de nivel superior es un sitio de administración central o un sitio primario independiente. Una vez completada la actualización de un sitio de administración central, puede actualizar los sitios primarios secundarios en cualquier orden que desee. Después de actualizar un sitio primario, puede actualizar sus sitios secundarios. También tiene la opción de actualizar sitios primarios adicionales antes de actualizar cualquier sitio secundario.  

Para actualizar un sitio de administración central o sitio primario, debe ejecutar el programa de instalación desde el medio de origen de System Center Configuration Manager. Sin embargo, no se ejecuta el programa de instalación para actualizar los sitios secundarios. En su lugar, se usa la consola de Configuration Manager para actualizar un sitio secundario después de completar la actualización de su sitio primario.  

Antes de actualizar un sitio, cierre la consola de Configuration Manager instalada en el servidor de sitio hasta que finalice la actualización del sitio. También debe cerrar cada consola de Configuration Manager que se ejecute en equipos que no sean el servidor de sitio. Puede volver a conectar la consola una vez completada la actualización del sitio. En cambio, hasta que actualice una consola de Configuration Manager a la nueva versión de Configuration Manager, esa consola no podrá mostrar algunos objetos ni información disponible en la nueva versión de Configuration Manager.  

Use los procedimientos siguientes para actualizar sitios de Configuration Manager:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Para actualizar un sitio de administración central o sitio primario  

1.  Compruebe que el usuario que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    -   Derechos de administrador local en el equipo del servidor de sitio.  
    -   Derechos de administrador local en el servidor de base de datos del sitio remoto para el sitio, si es remoto.    </br></br>

2.  En el equipo del servidor de sitio, abra el Explorador de Windows y vaya a **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Haga doble clic en **Setup.exe**. Se abre el Asistente para instalación de Configuration Manager.  

4.  En la página **Antes de empezar** , haga clic en **Siguiente**.  

5.  En la página **Introducción** , seleccione **Actualizar este sitio de Configuration Manager**y, a continuación, haga clic en **Siguiente**.  

6.  En la página **Clave de producto** , haga clic en **Siguiente**.  

     Si anteriormente ha instalado Configuration Manager Evaluation, puede seleccionar **Instalar la edición con licencia de este producto** y después escribir la clave de producto de la instalación completa de Configuration Manager para convertir el sitio en una versión completa.  

     A partir de la versión de octubre de 2016 de los medios de línea base de la versión 1606 para System Center Configuration Manager, puede especificar la fecha de expiración de su contrato de Software Assurance. También puede especificar la **fecha de expiración de Software Assurance** de su contrato de licencia como un cómodo recordatorio de esa fecha. Si no la especifica durante la instalación, puede especificarla más tarde desde la consola de Configuration Manager.

     >  [!NOTE]   
     >  Microsoft no valida la fecha de expiración que especifique y no la usará para la validación de la licencia,  pero usted puede usarla como un recordatorio de la fecha de expiración. Esto es útil porque Configuration Manager busca de forma periódica nuevas actualizaciones de software que se ofrecen en línea y el estado de su licencia de Software Assurance debe ser actual para que pueda usar estas actualizaciones adicionales.    

     Para obtener más información, consulte [Licencias y ramas para System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  En la página **Términos de licencia del software de Microsoft** , lea y acepte los términos de licencia y, a continuación, haga clic en **Siguiente**.  

8.  En la página **Licencias de requisitos previos** , lea y acepte los términos de licencia del software necesario y haga clic en **Siguiente**. El programa de instalación descarga e instala automáticamente el software en los sistemas de sitio o los clientes cuando sea necesario. Debe activar todas las casillas antes de continuar a la página siguiente.  

9. En la página **Descargas de requisitos previos** , especifique las descargas del programa de instalación y los archivos redistribuibles de requisitos previos, los paquetes de idioma y las últimas actualizaciones de producto desde Internet o use archivos descargados previamente y, a continuación, haga clic en **Siguiente**. Si previamente descargó los archivos con el descargador del programa de instalación, seleccione **Usar archivos descargados anteriormente** y especifique la carpeta de descarga. Para obtener más información, consulte [Descargador del programa de instalación](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Cuando se utilizan archivos descargados anteriormente, compruebe que la ruta de acceso a la carpeta de descarga contiene la versión más reciente de los archivos.  

10. En la página **Selección de idioma de servidor** , vea la lista de idiomas instalados actualmente para el sitio. Seleccione idiomas adicionales disponibles en este sitio para la consola de Configuration Manager y para los informes, o borre idiomas que ya no quiere en este sitio y después haga clic en **Siguiente**. De forma predeterminada, el inglés está seleccionado y no se puede quitar.  

    > [!IMPORTANT]  
    >  Las versiones de Configuration Manager no pueden usar paquetes de idioma de una versión anterior de Configuration Manager. Para habilitar la compatibilidad con un idioma en un sitio de Configuration Manager que actualice, debe usar la versión del paquete de idioma para esa nueva versión. Por ejemplo, durante la actualización de System Center 2012 Configuration Manager a System Center Configuration Manager, si la versión de System Center Configuration Manager de un paquete de idioma no está disponible con los archivos de requisitos previos que descargue, no se podrá instalar la compatibilidad con ese idioma.  

11. En la página **Selección de idioma de cliente** , vea la lista de idiomas instalados actualmente para el sitio. Seleccione los idiomas adicionales que están disponibles en este sitio para los equipos cliente o borre los idiomas que ya no desee admitir en este sitio. Especifique si desea habilitar todos los idiomas de cliente para clientes de dispositivos móviles y, a continuación, haga clic en **Siguiente**. De forma predeterminada, el inglés está seleccionado y no se puede quitar.  

    > [!IMPORTANT]  
    >  Las versiones de Configuration Manager no pueden usar paquetes de idioma de una versión anterior de Configuration Manager. Para habilitar la compatibilidad con un idioma en un sitio de Configuration Manager que actualice, debe usar la versión del paquete de idioma para esa nueva versión. Por ejemplo, durante la actualización de System Center 2012 Configuration Manager a System Center Configuration Manager, si la versión de System Center Configuration Manager de un paquete de idioma no está disponible con los archivos de requisitos previos que descargue, no se podrá instalar la compatibilidad con ese idioma.  

12. En la página **Resumen de configuración** , haga clic en **Siguiente** para iniciar el comprobador de requisitos y comprobar que el servidor está listo para la actualización del sitio.  

13. En la página **Comprobación de la instalación de requisitos previos** , si no se enumera ningún problema, haga clic en **Siguiente** para actualizar el sitio y los roles de sistema de sitio. Cuando el comprobador de requisitos previos encuentre un problema, haga clic en un elemento de la lista para obtener más información acerca de cómo resolver el problema. Resuelva todos los elementos de la lista que tengan un estado de **Error** antes de continuar el programa de instalación. Después de resolver el problema, haga clic en **Ejecutar comprobación** para reiniciar la comprobación de requisitos previos. También puede abrir el archivo ConfigMgrPrereq.log en la raíz de la unidad del sistema para revisar los resultados del comprobador de requisitos previos. El archivo de registro puede contener información adicional que no se muestra en la interfaz de usuario. Para obtener una lista de reglas de requisitos previos de instalación y descripciones, consulte [Comprobador de requisitos previos](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

En la página **Actualización** , el programa de instalación muestra el estado del progreso general. Una vez completada la instalación del servidor de sitio principal y del sistema de sitio, puede cerrar el asistente. La configuración del sitio continúa en segundo plano.  

#### <a name="to-upgrade-a-secondary-site"></a>Para actualizar un sitio secundario  

1.  Compruebe que el usuario administrativo que ejecuta el programa de instalación tenga los siguientes derechos de seguridad:  

    -   Derechos de administrador local en el equipo del sitio secundario  
    -   Rol de seguridad de administrador total o administrador de infraestructuras en el sitio primario  
    -   Derechos de administrador de sistema (SA) en la base de datos del sitio secundario  
    </br>
2.  En la consola de Configuration Manager, haga clic en **Administración**.  

3.  En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.  

4.  Seleccione el sitio secundario que desee actualizar y, a continuación, en la pestaña **Inicio** , en el grupo **Sitio** , haga clic en **Actualizar**.  

5.  Haga clic en **Sí** para confirmar la decisión y para iniciar la actualización del sitio secundario.  

La actualización del sitio secundario se ejecuta en segundo plano. Una vez completada la actualización, puede confirmar el estado en la consola de Configuration Manager. Para confirmar el estado, seleccione servidor del sitio secundario y, a continuación, en la pestaña **Inicio** , en el grupo **Sitio** , haga clic en **Mostrar estado de instalación**.  

##  <a name="BKMK_PostUpgrade"></a> Realizar tareas posteriores a la actualización  
Después de actualizar un sitio a un nuevo Service Pack, es posible que tenga que realizar tareas adicionales para finalizar la actualización o volver a configurar el sitio. Estas tareas pueden incluir: actualizar clientes de Configuration Manager o consolas de Configuration Manager, volver a habilitar réplicas de base de datos para puntos de administración o restaurar valores de configuración para funciones de Configuration Manager que use y que no permanezcan tras la actualización del Service Pack.  

**Problemas conocidos de los sitios secundarios:**  
- **Al actualizar a la versión 1511:** para asegurarse de que los clientes en sitios secundarios pueden encontrar el punto de administración desde el sitio secundario (punto de administración proxy), agregue de forma manual el punto de administración a los grupos de límites que también incluyen los puntos de distribución en el sitio secundario.  

- **Al actualizar a la versión 1606 o posteriores:** los puntos de administración proxy se agregan de forma automática a los grupos de límites que incluyen puntos de distribución en el sitio secundario.

