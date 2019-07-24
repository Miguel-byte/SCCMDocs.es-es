---
title: Información de administración
titleSuffix: Configuration Manager
description: Obtenga información sobre la funcionalidad Información de administración disponible en la consola de Configuration Manager.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17600d9fa04e678e488f36bb923a39e8c41647aa
ms.sourcegitcommit: b62de6c9cb1bc3e4c9ea5ab5ed3355d83e3a59bc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894099"
---
# <a name="management-insights-in-configuration-manager"></a>Información de administración en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Información de administración de Configuration Manager proporciona información sobre el estado actual del entorno. La información se basa en el análisis de los datos de la base de datos del sitio. Esta información le ayuda a entender mejor el entorno y tomar medidas en consecuencia. Esta característica se publicó en la versión 1802 de Configuration Manager. <!--1353967-->



## <a name="review-management-insights"></a>Revisar información de administración 

Para ver las reglas, su cuenta debe tener el permiso **leer** en el objeto **sitio**.

1. Abra la consola de Configuration Manager.  

2. Vaya al área de trabajo **Administración**, expanda **Información de administración** y seleccione **Toda la información**.  

    > [!Note]  
    > A partir de la versión 1810, al hacer clic en el nodo **Información de administración**, se muestra el [panel de información de administración](#bkmk_insights).  

3. Abra el grupo de información de administración que quiera revisar. Haga clic en **Mostrar información** en la cinta de opciones.  

Las siguientes cuatro pestañas están disponibles para su revisión: 

- **Todas las reglas**: proporciona la lista completa de las reglas para el grupo de información de administración elegido.  

- **Completa**:  enumera las reglas en las que no se necesita ninguna acción.  

- **En curso**: muestra las reglas en las que algunos requisitos previos están completos, pero no todos.  

- **Acción necesaria**: se enumeran las reglas en las que es necesario realizar acciones. Haga clic en **Más detalles** para recuperar los elementos específicos en los que se necesita una acción.  

El panel **Requisitos previos** muestra los elementos necesarios para ejecutar la regla.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Todas las reglas y requisitos previos para el grupo de servicios en la nube
![Información de administración: todas las reglas y requisitos previos para el grupo de servicios en la nube](./media/Management-insights-all-cloud-rules.png)


Seleccione una regla y después haga clic en **Más detalles** para ver los detalles de la regla.



## <a name="operations"></a>Operaciones

Las reglas de información de administración vuelven a evaluar su aplicabilidad de acuerdo a una programación semanal. Para volver a evaluar una regla a petición, haga clic con el botón derecho en la regla y seleccione **Reevaluar**.

El archivo de registro para reglas de información de administración es **SMS_DataEngine.log** en el servidor de sitio.

<!--1357930-->
A partir de la versión 1806, algunas reglas le permiten tomar medidas. Seleccione una regla y haga clic en **Más detalles**. Después, si está disponible, seleccione **Tomar medidas**. 

En función de la regla, esta acción muestra uno de los siguientes comportamientos:  

- Navegar automáticamente por la consola hasta el nodo donde se puede realizar una acción. Por ejemplo, si la información de administración recomienda cambiar una configuración de cliente, al llevar a cabo la acción navegará hasta el nodo Configuración de cliente. Después realice otra acción modificando los valores predeterminados o un objeto de configuración de cliente personalizado.  

- Navegar a una vista filtrada basándose en una consulta. Por ejemplo, al actuar en la regla de recopilaciones vacías se muestran solo estas recopilaciones en la lista de recopilaciones. Después puede realizar otra acción, como eliminar una recopilación o modificar sus reglas de pertenencia.  



## <a name="bkmk_insights"></a> Panel de información de administración
<!--1357979-->

A partir de la versión 1810, el nodo **Información de administración** incluye un panel gráfico. Este panel muestra información general de los estados de la regla, con lo que le resultará más fácil mostrar el progreso. 

Use los siguientes filtros en la parte superior del panel para ajustar la vista:
- Mostrar completadas
- Opcional
- Recomendado
- Crítica

En el panel se incluyen los iconos siguientes:  

- **Índice de Información de administración**: realiza el seguimiento del progreso general en las reglas de información de administración. El índice es un promedio ponderado. Las reglas críticas valen más. Este índice proporciona el menor peso a las reglas opcionales.  

- **Grupos de Información de administración**: muestra el porcentaje de las reglas en cada grupo, teniendo en cuenta los filtros. Seleccione un grupo para explorar en profundidad las reglas específicas de este grupo.  

- **Prioridad de Información de administración**: muestra el porcentaje de las reglas por prioridad, teniendo en cuenta los filtros.   

- **Toda la información**: una tabla de información, incluida la prioridad y el estado. Use el campo **Filtro** situado en la parte superior de la tabla para emparejar las cadenas de cualquiera de las columnas disponibles. El panel ordena la tabla en el orden siguiente:
    - Estado: acción necesaria, completado, desconocido  
    - Prioridad: crítica, recomendada, opcional  
    - Último cambio: fechas más antiguas en la parte superior   

![Captura de pantalla del panel de información de administración](media/1357979-management-insights-dashboard.png)



## <a name="groups-and-rules"></a>Reglas y grupos

Las reglas se organizan en los siguientes grupos de información de administración:
- [Aplicaciones](#applications)  
- [Servicios en la nube](#cloud-services)  
- [Recopilaciones](#collections)  
- [Mantenimiento proactivo](#proactive-maintenance)  
- [Seguridad](#security)  
- [Administración simplificada](#simplified-management)  
- [Centro de software](#software-center)  
- [Windows 10](#windows-10)  


### <a name="applications"></a>Aplicaciones

Conclusiones de administración de la aplicación.

- **Aplicaciones sin implementaciones**: enumera las aplicaciones del entorno sin implementaciones activas. Esta regla ayuda a encontrar y eliminar las aplicaciones sin usar para simplificar la lista de aplicaciones que se muestran en la consola. Para obtener más información, consulte [Deploy applications](/sccm/apps/deploy-use/deploy-applications) (Implementar aplicaciones).  


### <a name="cloud-services"></a>Servicios en la nube

Ayuda a integrar con muchos servicios en la nube, lo que permite la administración moderna de los dispositivos. 

- **Evaluar la preparación de la administración conjunta**: ayuda a comprender qué pasos son necesarios para habilitar la administración conjunta. Esta regla tiene requisitos previos. Para obtener más información, vea [Información general sobre la administración conjunta](/sccm/comanage/overview).  

- **Configuración de servicios de Azure para utilizarlos con Configuration Manager**: esta regla le ayuda a incorporar Configuration Manager a Azure AD, que permite a los clientes autenticarse en el sitio mediante Azure AD. Para obtener más información, vea [Configuración de servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Habilitar dispositivos para que sean híbridos unidos a Azure Active Directory**: los dispositivos unidos a Azure AD permiten a los usuarios iniciar sesión con sus credenciales de dominio y también asegurarse de que los dispositivos cumplen los estándares de seguridad y cumplimiento de la organización. Para obtener más información, vea [Consideraciones de diseño de identidad híbrida de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Actualización de clientes a la versión más reciente de Windows 10**: Windows 10, versión 1709 o superior, mejora y moderniza la experiencia informática de los usuarios. Para obtener más información, vea [Artículos clave sobre la adopción de Windows como servicio](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Recopilaciones

Información que ayuda a simplificar la administración mediante la limpieza y reconfiguración de las colecciones.

- **Colecciones vacías**: enumera las colecciones del entorno que no tienen miembros. Para obtener más información, vea [Cómo administrar colecciones](/sccm/core/clients/manage/collections/manage-collections).  

A partir de la versión 1902, hay nuevas reglas con recomendaciones sobre la administración de colecciones.<!--3555752--> Use esta información para simplificar la administración y mejorar el rendimiento:

- **Colecciones con ninguna regla de consulta y ningún miembro directo**: elimine estas colecciones para simplificar la lista de colecciones de la jerarquía.  

- **Colecciones con la misma hora de inicio de reevaluación**: estas colecciones tienen la misma hora de reevaluación que otras colecciones. Modifique la hora de reevaluación para que no entren en conflicto.  

- **Colecciones con tiempo de consulta superior a dos segundos**: revise las reglas de consulta de esta colección. Considere la posibilidad de modificar o eliminar la colección.

- Estas reglas incluyen configuraciones que podrían ocasionar una carga innecesaria en el sitio. Revise estas colecciones y elimínelas o deshabilite la evaluación de regla:  

    - **Colecciones sin reglas de consulta y actualizaciones incrementales habilitadas**  

    - **Colecciones sin reglas de consulta y habilitadas para la evaluación incremental o programada**  

    - **Colecciones sin reglas de consulta y con una evaluación completa programada seleccionada**  


### <a name="proactive-maintenance"></a>Mantenimiento proactivo
<!--1352184-->
A partir de la versión 1806, las reglas de este grupo resaltan posibles problemas de configuración que puede evitar mediante el mantenimiento de los objetos de Configuration Manager. 

- **Grupos de límites sin sistemas de sitio asignados**: sin los sistemas de sitio asignados, los grupos de límites solo pueden usarse para la asignación de sitio. Para obtener más información, vea [Configuración de grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Grupos de límites sin miembros**: los grupos de límites no son aplicables a la asignación de sitio o a la búsqueda de contenido si no tienen ningún miembro. Para obtener más información, vea [Configuración de grupos de límites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Puntos de distribución que no proporcionan contenido a los clientes**: puntos de distribución que no han proporcionado contenido a los clientes en los treinta últimos días. Estos datos se basan en los informes de los clientes de su historial de descargas. Para obtener más información, vea [Instalación y configuración de puntos de distribución](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Habilitar la limpieza WSUS**: comprueba que haya habilitado la opción para ejecutar la limpieza WSUS en las propiedades de componente de punto de actualización de software. Esta opción ayuda a mejorar el rendimiento de WSUS. Para obtener más información, vea [Mantenimiento de las actualizaciones de software](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Imágenes de arranque no utilizadas**: imágenes de arranque a las que no hay ninguna referencia para el uso de la secuencia de tareas o del arranque PXE. Para más información, vea [Manage boot images (Administrar imágenes de arranque)](/sccm/osd/get-started/manage-boot-images).  

- **Elementos de configuración no utilizados**: elementos de configuración que no forman parte de una línea base de configuración y tienen más de 30 días. Para obtener más información, consulte [Crear una línea base de configuración](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Actualizar los orígenes de caché del mismo nivel a la última versión del cliente de Configuration Manager**: indentifique a los clientes que actúan como origen de caché del mismo nivel, pero no se ha actualizado desde una versión del cliente anterior a la 1806. Los clientes de la versión anterior a la 1806 no pueden usarse como un origen de caché del mismo nivel para clientes que ejecutan la versión 1806 o alguna posterior. Seleccione **Realizar acción** para abrir una vista de dispositivo que muestre la lista de clientes.<!--1358008-->  


### <a name="security"></a>Seguridad
Conclusiones para mejorar la seguridad de su infraestructura y dispositivos. 

- **Versiones del cliente antimalware no admitidas**: Más del 10 % de los clientes ejecutan versiones de System Center Endpoint Protection que no son compatibles. Para obtener más información, vea [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Administración simplificada

Conclusiones que le ayudarán a simplificar la administración diaria de su entorno. 

- **Versiones de cliente diferentes de CB**: enumera todos los clientes cuyas versiones no son una compilación de la rama actual (CB). Para obtener más información, vea [Actualizar clientes](/sccm/core/clients/manage/upgrade/upgrade-clients).  

- **Actualizar clientes a una versión de Windows 10 admitida**: a partir de la versión 1902, esta regla informa sobre los clientes que ejecutan una versión de Windows 10 que ya no se admite. También incluye a los clientes con una versión de Windows 10 que se acerca al final del servicio (tres meses).<!--3897268-->  


### <a name="software-center"></a>Centro de software

Conclusiones para la administración del Centro de software. 

- **Dirigir a los usuarios al Centro de software en lugar de al catálogo de aplicaciones**: compruebe si los usuarios han instalado o solicitado aplicaciones del catálogo de aplicaciones en los últimos 14 días. La funcionalidad principal del Catálogo de aplicaciones ahora se incluye en el Centro de software. La compatibilidad con el sitio web del catálogo de aplicaciones finaliza en la versión 1806. Para más información, vea [Deprecated Features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features) (Características en desuso).  

- **Uso de la nueva versión del Centro de software**: La versión anterior del Centro de software ya no se admite. Configure los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Usar nuevo Centro de software** en el grupo **Agente de equipo**. Para más información, vea [Acerca de la configuración de cliente](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  


### <a name="windows-10"></a>Windows 10

Conclusiones relacionadas con la implementación y el mantenimiento de Windows 10. El grupo de información de administración de Windows 10 está solo disponible cuando más de la mitad de los clientes ejecutan Windows 7, Windows 8 o Windows 8.1.

- **Configurar la telemetría de Windows y la clave de id. comercial**: para usar datos de Upgrade Readiness, configure los dispositivos con una clave de id. comercial y habilite la telemetría. Establezca los dispositivos Windows 10 en el nivel de telemetría Mejorado (limitado) o en uno superior. Para obtener más información, vea [Configuración de clientes para notificar datos a Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Conexión de Configuration Manager con Upgrade Readiness**: aproveche Upgrade Readiness para agilizar sus implementaciones de Windows 10 antes de que Windows 7 se quede sin soporte. Para obtener más información, vea [Integrar Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Reglas de información de administración de Windows 10
![Reglas de información de administración para Windows 10](./media/Windows-10-insights-group.png)
