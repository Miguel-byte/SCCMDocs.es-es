---
title: "Conceptos básicos de la administración basada en roles | System Center Configuration Manager"
description: "Use la administración basada en roles para controlar el acceso administrativo a Configuration Manager y a los objetos que administra."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3e70794144caa5a1993cc65089b1076476fc6106


---
# <a name="fundamentals-of-role-based-administration-for-system-center-configuration-manager"></a>Conceptos básicos de la administración basada en roles de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con System Center Configuration Manager se usa la administración basada en roles para proteger el acceso para administrar Configuration Manager, y los objetos que se administran como recopilaciones, implementaciones y sitios.   Una vez que comprenda los conceptos presentados en este tema, podrá [Configure role-based administration for System Center Configuration Manager (Configurar la administración basada en roles para System Center Configuration Manager)](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 El modelo de administración basada en roles define y administra de manera centralizada la configuración de acceso de seguridad de la totalidad de la jerarquía para todos los sitios y sus configuraciones, mediante lo siguiente:  

-   **Roles de seguridad** : se asignan a los usuarios administrativos para proporcionar a dichos usuarios (o grupos de usuarios) permisos de diferentes objetos de Configuration Manager, tales como los permisos para crear o cambiar la configuración de cliente.  

-   **Ámbitos de seguridad** : agrupan instancias específicas de objetos que un usuario administrativo se encarga de administrar, por ejemplo, una aplicación que instala Microsoft Office 2010.  

-   **Recopilaciones** : grupos de recursos de usuarios y de dispositivos que el usuario administrativo puede administrar.  

 La combinación de roles de seguridad, ámbitos de seguridad y recopilaciones permite segregar las asignaciones administrativas que satisfacen las necesidades de la organización y, juntos, definen el ámbito administrativo de un usuario (lo que el usuario puede ver y administrar en la implementación de Configuration Manager).  

**La administración basada en roles proporciona las siguientes ventajas:**  

-   Los sitios no se usan como límites administrativos.  

-   Puede crear usuarios administrativos para una jerarquía y solo es necesario asignarles la seguridad una vez.  

-   Todas las asignaciones de seguridad se replican y están disponibles en toda la jerarquía.  

-   Hay varios roles de seguridad integrados para asignar las tareas administrativas habituales y puede crear sus propios roles de seguridad personalizados para satisfacer sus requisitos empresariales.  

-   Los usuarios administrativos solo ven los objetos para los que tienen permisos de administración.  

-   Puede auditar las acciones de seguridad administrativa.  

Al diseñar e implementar la seguridad administrativa de Configuration Manager, se usa lo siguiente para crear un **ámbito administrativo** para un usuario administrativo:  

-   [Roles de seguridad](#bkmk_Planroles)  

-   [Recopilaciones](#bkmk_planCol)  

-   [Ámbitos de seguridad](#bkmk_PlanScope)  

 El ámbito administrativo controla los objetos que un usuario administrativo puede ver en la consola de Configuration Manager y los permisos que el usuario tiene en dichos objetos. Las configuraciones de administración basada en roles se replican en cada sitio en la jerarquía como datos globales y, a continuación, se aplican a todas las conexiones administrativas.  

> [!IMPORTANT]  
>  Los retrasos de replicación entre sitios pueden impedir que un sitio reciba los cambios de la administración basada en roles. Para obtener más información sobre cómo supervisar la replicación de base de datos entre sitios, consulte el tema [Transferencias de datos entre sitios en System Center Configuration Manager](../../core/servers/manage/data-transfers-between-sites.md).  

##  <a name="a-namebkmkplanrolesa-security-roles"></a><a name="bkmk_Planroles"></a> Roles de seguridad  
 Use roles de seguridad para conceder permisos de seguridad a usuarios administrativos. Los roles de seguridad son grupos de permisos de seguridad que se asignan a usuarios administrativos para que puedan realizar sus tareas administrativas. Estos permisos de seguridad definen las acciones administrativas que un usuario administrativo puede realizar y los permisos que se conceden para determinados tipos de objetos. Como medida de seguridad recomendada, asigne roles de seguridad que proporcionen el menor nivel de permisos.  

 Configuration Manager dispone de varios roles de seguridad integrados para admitir las agrupaciones habituales de tareas administrativas. Puede crear sus propios roles de seguridad para satisfacer sus requisitos empresariales. Ejemplos de roles de seguridad integrados:  

-   **Administrador total**: este rol de seguridad concede todos los permisos en Configuration Manager.  

-   **Analista de activos**: este rol de seguridad permite a los usuarios administrativos ver los datos recopilados mediante Asset Intelligence, inventario de software, inventario de hardware y medición de software. Los usuarios administrativos pueden crear reglas de compatibilidad y categorías, familias y etiquetas de Asset Intelligence.  

-   **Administrador de actualizaciones de software**: este rol de seguridad concede permisos para definir e implementar actualizaciones de software. Los usuarios administrativos asociados a este rol pueden crear recopilaciones, grupos de actualizaciones de software, implementaciones y plantillas, y habilitar actualizaciones de software para Protección de acceso a redes (NAP).  

> [!TIP]  
>  Puede ver la lista de los roles de seguridad integrados y los roles de seguridad personalizados que crea, y sus descripciones, en la consola de Configuration Manager. A tal efecto, en el área de trabajo **Administración** , expanda **Seguridad**y, a continuación, haga clic en **Roles de seguridad**.  

 Cada rol de seguridad tiene determinados permisos para distintos tipos de objetos. Por ejemplo, el rol de seguridad **Administrador de aplicaciones** tiene los siguientes permisos para las aplicaciones: **Aprobar**, **Crear**, **Eliminar**, **Modificar**, **Modificar carpetas**, **Mover objetos**, **Leer/Implementar**, **Establecer ámbito de seguridad**. No puede cambiar los permisos de los roles de seguridad integrados, pero puede copiar el rol, realizar cambios y, a continuación, guardar estos cambios como un nuevo rol de seguridad personalizado. También puede importar roles de seguridad que ha exportado desde otra jerarquía (por ejemplo, de una red de prueba). Revise los roles de seguridad y sus permisos para determinar si utilizará los roles de seguridad integrados o si debe crear sus propios roles de seguridad personalizados.  

 **Los pasos siguientes le ayudan a planear los roles de seguridad:**  

1.  Identifique las tareas que los usuarios administrativos realizan en Configuration Manager. Estas tareas pueden estar relacionadas con uno o más grupos de tareas de administración, como la implementación de aplicaciones y paquetes, la implementación de sistemas operativos y configuraciones para el cumplimiento, la configuración de sitios y seguridad, la realización de auditorías, el control remoto de equipos y la recopilación de datos de inventario.  

2.  Asigne estas tareas administrativas a uno o varios roles de seguridad integrados.  

3.  Si algunos de los usuarios administrativos realiza las tareas de varios roles de seguridad, asigne dichos roles de seguridad a estos usuarios administrativos en vez de crear un nuevo rol de seguridad que combine las tareas.  

4.  Si las tareas que identificó no se ajustan a los roles de seguridad integrados, cree y pruebe nuevos roles de seguridad.  

Para obtener más información sobre cómo crear y configurar roles de seguridad para la administración basada en roles, consulte [Crear roles de seguridad personalizados](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) y [Configurar roles de seguridad](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) en el tema [Configure role-based administration for System Center Configuration Manager (Configurar la administración basada en roles para System Center Configuration Manager)](../../core/servers/deploy/configure/configure-role-based-administration.md).  

##  <a name="a-namebkmkplancola-collections"></a><a name="bkmk_planCol"></a> Recopilaciones  
 Las recopilaciones especifican los recursos de usuario y equipo que los usuarios administrativos pueden ver o administrar. Por ejemplo, para que los usuarios administrativos puedan implementar aplicaciones o ejecutar el control remoto, deben estar asignados a un rol de seguridad que conceda acceso a la recopilación que contiene dichos recursos. Puede seleccionar recopilaciones de usuarios o dispositivos.  

 Para obtener más información sobre las recopilaciones, consulte [Introduction to collections in System Center Configuration Manager (Introducción a las recopilaciones en System Center Configuration Manager)](../../core/clients/manage/collections/introduction-to-collections.md).  

 Antes de configurar la administración basada en roles, compruebe si tiene que crear nuevas recopilaciones por cualquiera de las siguientes razones:  

-   Organización funcional. Por ejemplo, separar recopilaciones de servidores y estaciones de trabajo.  

-   Alineación geográfica. Por ejemplo, separar recopilaciones de Europa y América del Norte.  

-   Requisitos de seguridad y procesos empresariales. Por ejemplo, separar las recopilaciones para equipos de prueba y producción.  

-   Alineación de la organización. Por ejemplo, separar recopilaciones para cada unidad de negocio.  

Para obtener más información sobre cómo configurar recopilaciones para la administración basada en roles, consulte [Configurar recopilaciones para administrar la seguridad](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) en el tema [Configure role-based administration for System Center Configuration Manager (Configurar la administración basada en roles para System Center Configuration Manager)](../../core/servers/deploy/configure/configure-role-based-administration.md) .  

##  <a name="a-namebkmkplanscopea-security-scopes"></a><a name="bkmk_PlanScope"></a> Ámbitos de seguridad  
 Use los ámbitos de seguridad para proporcionar acceso a objetos protegibles para los usuarios administrativos. Los ámbitos de seguridad son un conjunto de objetos protegibles asignados a usuarios administrativos como un grupo. Todos los objetos protegibles deben estar asignados a uno o más ámbitos de seguridad. Configuration Manager tiene dos ámbitos de seguridad integrados:  

-   **Todo**: este ámbito de seguridad integrado concede acceso a todos los ámbitos. No se pueden asignar objetos a este ámbito de seguridad.  

-   **Predeterminado**: este ámbito de seguridad integrado se usa para todos los objetos de forma predeterminada. Cuando se instala inicialmente Configuration Manager, todos los objetos se asignan a este ámbito de seguridad.  

Si desea restringir los objetos que los usuarios administrativos pueden ver y administrar, debe crear y utilizar sus propios ámbitos de seguridad personalizados. Los ámbitos de seguridad no admiten estructuras jerárquicas y no se pueden anidar. Los ámbitos de seguridad pueden contener uno o varios tipos de objetos, como:  

-   Suscripciones de alerta  

-   Aplicaciones  

-   Imágenes de arranque  

-   Grupos de límites  

-   Elementos de configuración  

-   Configuraciones personalizadas de cliente  

-   Puntos de distribución y grupos de puntos de distribución  

-   Paquetes de controladores  

-   Condiciones globales  

-   Trabajos de migración  

-   Imágenes de sistema operativo  

-   Paquetes de instalación de sistema operativo  

-   Paquetes  

-   Consultas  

-   Sitios  

-   Reglas de disponibilidad de software  

-   Grupos de actualizaciones de software  

-   Paquetes de actualizaciones de software  

-   Paquetes de secuencias de tareas  

-   Paquetes y elementos de configuración de dispositivos Windows CE  

También hay algunos objetos que no se incluyen en los ámbitos de seguridad ya que solo se pueden proteger mediante roles de seguridad. El acceso administrativo a estos objetos no se puede limitar a un subconjunto de los objetos disponibles. Por ejemplo, puede tener un usuario administrativo que crea grupos de límites que se utilizan en un determinado sitio. Ya que el objeto de límite no admite ámbitos de seguridad, no puede asignar al usuario un ámbito de seguridad que solo proporciona acceso a los límites que puedan estar asociados a ese sitio. Como los objetos de límite no pueden estar asociados a un ámbito de seguridad, cuando asigna un rol de seguridad que incluye el acceso a objetos de límite a un usuario, el usuario puede obtener acceso a todos los límites de la jerarquía.  

Entre los objetos que no están limitados por ámbitos de seguridad se incluyen los siguientes:  

-   Bosques de Active Directory  

-   Usuarios administrativos  

-   Alertas  

-   Directivas antimalware  

-   Límites  

-   Asociaciones de equipos  

-   Configuración de cliente predeterminada  

-   Plantillas de implementación  

-   Controladores de dispositivo  

-   Conector de Exchange Server  

-   Asignaciones de sitio a sitio de migración  

-   Perfiles de inscripción de dispositivo móvil  

-   Roles de seguridad  

-   Ámbitos de seguridad  

-   Direcciones de sitios  

-   Roles de sistema de sitio  

-   Títulos de software  

-   Actualizaciones de software  

-   Mensajes de estado  

-   Afinidades de dispositivo de usuario  

Cree ámbitos de seguridad si tiene que limitar el acceso a instancias independientes de objetos. Por ejemplo:  

-   Un grupo de usuarios administrativos tiene que poder ver las aplicaciones de producción pero no tiene que poder ver aplicaciones de prueba. Cree un ámbito de seguridad para las aplicaciones de producción y otro para las aplicaciones de prueba.  

-   Los distintos usuarios administrativos requieren un determinado acceso a algunas instancias de un tipo de objeto. Por ejemplo, un grupo de usuarios administrativos requiere el permiso **Leer** en determinados grupos de actualizaciones de software, y otro grupo de usuarios administrativos requiere el permiso **Modificar** y **Eliminar** para otros grupos de actualizaciones de software. Cree distintos ámbitos de seguridad para estos grupos de actualizaciones de software.  

Para obtener más información sobre cómo configurar ámbitos de seguridad para la administración basada en roles, consulte [Configurar ámbitos de seguridad para un objeto](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) en el tema [Configure role-based administration for System Center Configuration Manager (Configurar la administración basada en roles para System Center Configuration Manager)](../../core/servers/deploy/configure/configure-role-based-administration.md).  



<!--HONumber=Nov16_HO1-->

