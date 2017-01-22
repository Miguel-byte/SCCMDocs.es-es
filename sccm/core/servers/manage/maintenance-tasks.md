---
title: Tareas de mantenimiento | Microsoft Docs
description: "Obtenga información sobre las tareas de mantenimiento que deben llevarse a cabo para las jerarquías y los sitios de Configuration Manager y los momentos en que deben realizarse."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 46a24145d28111d7611f393f5806d0d7cc47ed71


---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tareas de mantenimiento para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Los sitios y las jerarquías de System Center Configuration Manager requieren mantenimiento regular y supervisión a fin de proporcionar servicios de forma efectiva y continua. El mantenimiento regular asegura de que el hardware, el software y la base de datos de Configuration Manager funcionan de manera correcta y eficaz. Un rendimiento óptimo reduce en gran medida el riesgo de error.  

 Para configurar alertas y usar el sistema de estado para supervisar el estado de Configuration Manager, consulte [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md) (Uso de alertas y el sistema de estado para System Center Configuration Manager).  

-   [Tareas de mantenimiento](#bkmk_MTs)  

##  <a name="a-namebkmkmtsa-maintenance-tasks"></a><a name="bkmk_MTs"></a> Tareas de mantenimiento  
 Es importante realizar un mantenimiento regular para garantizar las operaciones correctas en el sitio. Debe mantenerse un registro de mantenimiento para documentar las fechas de realización del mantenimiento, quién lo realizó y cualquier comentario relacionado con el mantenimiento sobre la tarea realizada.  

### <a name="when-to-perform-common-maintenance-tasks"></a>Cuándo se deben realizar las tareas comunes de mantenimiento  
 Para realizar el mantenimiento del sitio, considere la posibilidad de realizar un mantenimiento regular de forma diaria, semanal y, en algunas tareas, una programación más periódica. El mantenimiento común puede incluir tareas de mantenimiento integradas y otras tareas, como el mantenimiento de cuentas para cumplir con las directivas de la empresa.  

 Utilice la siguiente información como guía para ayudarle a planear el momento adecuado para realizar las distintas tareas de mantenimiento. Utilice estas listas como punto de partida y agregue cualquier tarea adicional que pueda necesitar.  

**Tareas diarias**   
A continuación se indican las tareas de mantenimiento que puede realizar a diario:  

-   Compruebe que las tareas de mantenimiento predefinidas, programadas para ejecutarse a diario, se ejecutan correctamente.  

-   Compruebe el estado de la base de datos de Configuration Manager  

-   Compruebe el estado del servidor de sitio.  

-   Compruebe si existen archivos pendientes en las bandejas de entrada del sistema de sitio de Configuration Manager  

-   Compruebe el estado de los sistemas de sitio.  

-   Compruebe los registros de eventos del sistema operativo en sistemas de sitio.  

-   Compruebe el registro de errores de SQL Server en el equipo de base de datos del sitio.  

-   Compruebe el rendimiento del sistema.  

-   Administración de alertas de Configuration Manager  

**Tareas semanales**   
A continuación se indican las tareas de mantenimiento que puede realizar semanalmente:  

-   Compruebe que las tareas de mantenimiento predefinidas, programadas para ejecutarse semanalmente, se ejecutan correctamente.  

-   Elimine los archivos innecesarios de los sistemas de sitio.  

-   Produzca y distribuya informes del usuario final, si fuera necesario.  

-   Realice una copia de seguridad de los registros de eventos de la aplicación, la seguridad y el sistema, y bórrelos.  

-   Compruebe el tamaño de la base de datos de sitio y compruebe que hay suficiente espacio en disco disponible en el servidor de base de datos del sitio para que pueda aumentar la base de datos del sitio.  

-   Realice el mantenimiento de la base de datos de SQL Server en la base de datos del sitio, según su plan de mantenimiento de SQL Server.  

-   Compruebe el espacio en disco disponible en todos los sistemas de sitio.  

-   Ejecute las herramientas de desfragmentación de disco en todos los sistemas de sitio.  

**Tareas periódicas**   
Algunas tareas no hay que realizarlas durante el mantenimiento diario o semanal, sino que son importantes para asegurar el estado general del sitio, así como para asegurarse de que los planes de recuperación ante desastres y de seguridad están actualizados. Estas son las tareas de mantenimiento que pueden realizarse de forma más periódica que las tareas diarias o semanales:  

-   Cambie las cuentas y contraseñas, si es necesario, según el plan de seguridad.  

-   Revise el plan de mantenimiento para comprobar que las tareas de mantenimiento programado se programan de manera correcta y eficaz, en función de las opciones del sitio configurado.  

-   Revise los cambios requeridos en el diseño de la jerarquía de Configuration Manager  

-   Compruebe el rendimiento de red para asegurarse de que no se realizaron cambios que afectan a las operaciones del sitio.  

-   Compruebe que no cambió la configuración de Active Directory que afecta a las operaciones del sitio. Por ejemplo, compruebe que no cambiaron las subredes asignadas a los sitios de Active Directory que se utilizan como límites para el sitio de Configuration Manager.  

-   Revise los cambios necesarios en su plan de recuperación ante desastres.  

-   Realice una recuperación del sitio de acuerdo con el plan de recuperación ante desastres en un laboratorio de pruebas mediante una copia de seguridad de la copia de seguridad más reciente creada por la tarea de mantenimiento Copia de seguridad del servidor del sitio.  

-   Compruebe si hay algún error en el hardware o si hay actualizaciones de hardware disponibles.  

-   Compruebe el estado general del sitio.  

###  <a name="a-namebkmkusemtsa-maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Mantenimiento del estado operativo de la base de datos  
 Mientras el sitio y la jerarquía de Configuration Manager ejecutan las tareas que el usuario programa y configura, los componentes de sitio agregan continuamente datos a la base de datos de Configuration Manager. A medida que aumenta la cantidad de datos, disminuye el rendimiento de la base de datos y el espacio de almacenamiento libre de la base de datos. Puede configurar las tareas de mantenimiento de sitio para quitar los datos antiguos que ya no necesita.  

 Configuration Manager proporciona tareas de mantenimiento predefinidas que puede usar para mantener el estado de la base de datos de Configuration Manager. De forma predeterminada, no todas las tareas de mantenimiento están disponibles en cada sitio; algunas están habilitadas y otras no, y todas ellas admiten una programación que puede configurar para cuando se ejecuten.  

 La mayoría de las tareas de mantenimiento quitan periódicamente datos obsoletos de la base de datos de Configuration Manager. La reducción del tamaño de la base de datos mediante la supresión de datos innecesarios mejora el rendimiento y la integridad de la base de datos, lo que aumenta la eficacia de la jerarquía y del sitio. Otras tareas, como **Recompilar índices**, permiten mantener la eficacia de la base de datos mientras que otras, como la tarea **Copia de seguridad del servidor del sitio** , le preparan para la recuperación ante desastres.  

> [!IMPORTANT]  
>  Al planear la programación de cualquier tarea que elimina datos, considere el uso de los datos en la jerarquía. Cuando una tarea que elimina los datos se ejecuta en un sitio, la información se quita de la base de datos de Configuration Manager, y este cambio se replica en todos los sitios de la jerarquía. Esto puede afectar a otras tareas que dependen de esos datos. Por ejemplo, en el sitio de administración central, el usuario puede configurar la detección para que se ejecute una vez al mes con objeto de identificar equipos no clientes y planear la instalación del cliente de Configuration Manager para estos equipos en menos de dos semanas de su detección. Sin embargo, en un sitio de la jerarquía, un administrador configura la tarea Eliminar datos de detección antiguos para que se ejecute cada siete días, y que siete días después de detectados los equipos no cliente se eliminen de la base de datos de Configuration Manager. En el sitio de administración central, prepare la instalación de inserción del cliente de Configuration Manager en estos equipos nuevos el día 10. Sin embargo, como se había ejecutado la tarea Eliminar datos de detección antiguos y había eliminado datos a partir de siete días de antigüedad, esos equipos recientemente detectados ya no están disponibles en la base de datos.  

Después de instalar un sitio de Configuration Manager, revise las tareas de mantenimiento disponibles y habilite las tareas que requieren sus operaciones. Revise la programación predeterminada de cada tarea y, cuando sea necesario, modifique la programación para refinar la tarea de mantenimiento para que se ajuste a su entorno y jerarquía. Aunque la programación predeterminada de cada tarea debe adaptarse a la mayoría de los entornos, supervise el rendimiento de los sitios y de la base de datos, y refine las tareas para aumentar la eficacia de las implementaciones. Tenga prevista la revisión periódica del rendimiento del sitio y de la base de datos, y vuelva a configurar las tareas de mantenimiento y sus programaciones para mantener esa eficacia.  

#### <a name="configure-maintenance-tasks"></a>Configure tareas de mantenimiento.  
 Cada sitio de Configuration Manager admite tareas de mantenimiento que ayudan a mantener la eficiencia operativa de la base de datos del sitio. De forma predeterminada, se habilitan varias tareas de mantenimiento en cada sitio y todas las tareas compatibles con programaciones independientes. Tareas de mantenimiento se configuran individualmente para cada sitio y se aplican a la base de datos en el sitio; Sin embargo, algunas tareas, como **Eliminar datos de detección antiguos**, afectan a la información disponible en todos los sitios de una jerarquía.  

 Solo las tareas de mantenimiento que se pueden configurar en un sitio se muestran en la consola de Configuration Manager. Para obtener una lista completa de las tareas de mantenimiento por tipo de sitio, consulte [Reference for maintenance tasks for System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md) (Referencia para tareas de mantenimiento para System Center Configuration Manager).  

 Utilice el procedimiento siguiente para ayudarle a configurar la configuración común de tareas de mantenimiento.  

###### <a name="to-configure-maintenance-tasks-for-configuration-manager"></a>Para configurar las tareas de mantenimiento de Configuration Manager  

1.  En la consola de Configuration Manager, vaya a **Administración** > **Configuración del sitio** >**Sitios**.  

2.  Seleccione el sitio que contiene la tarea de mantenimiento que desea configurar.  

3.  En el **Inicio** ficha el **configuración de** de grupo, haga clic en **Mantenimiento del sitio**, y, a continuación, seleccione la tarea de mantenimiento que desea configurar.  

    > [!TIP]  
    >  Se muestran únicamente las tareas disponibles en el sitio seleccionado.  

4.  Para configurar la tarea, haga clic en **Editar**, garantizar la **habilitar esta tarea** casilla de verificación está seleccionada y configurar una programación para cuando se ejecuta la tarea. Si la tarea también elimina los datos antiguos, configure la antigüedad de los datos que se eliminarán de la base de datos cuando se ejecuta la tarea. Haga clic en **Aceptar** para cerrar la tarea **propiedades**.  

    > [!NOTE]  
    >  Para **Eliminar mensajes de estado antiguos**, configurar la antigüedad de los datos para eliminar al configurar reglas de filtro de estado.  

5.  Para habilitar o deshabilitar la tarea sin necesidad de editar las propiedades de la tarea, haga clic en el **Habilitar** o **deshabilitar** botón. El botón etiqueta cambia según la configuración actual de la tarea.  

6.  Cuando haya terminado de configurar las tareas de mantenimiento, haga clic en **Aceptar** para completar el procedimiento.



<!--HONumber=Dec16_HO3-->


