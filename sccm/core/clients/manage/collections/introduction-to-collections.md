---
title: "Introducción a las recopilaciones | System Center Configuration Manager"
description: "Obtenga una introducción para usar las recopilaciones en System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introducción a las recopilaciones en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Las recopilaciones en System Center Configuration Manager le proporcionan los medios para organizar los recursos en unidades administrables que, a su vez, le permiten crear una estructura organizada que represente lógicamente los tipos de tareas que quiere realizar. Las recopilaciones se usan también para realizar las operaciones de Configuration Manager en varios recursos al mismo tiempo. La tabla siguiente muestra algunos ejemplos de cómo puede usar las recopilaciones en Configuration Manager:  

|Operación|Ejemplo|  
|---------|-------|  
|Agrupación de recursos|Puede crear recopilaciones que agrupen de manera lógica recursos que se basan en la jerarquía de la organización.<br /><br /> Por ejemplo, podría crear una recopilación de todos los equipos que residen en la unidad organizativa (UO) de Active Directory "oficina central de Londres". Para obtener más información sobre cómo crear este tipo de colección, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Después, podría usar esta recopilación para realizar operaciones como la configuración de Endpoint Protection, configurar opciones de administración de energía de dispositivos o instalar el cliente de Configuration Manager.|  
|Implementación de aplicaciones|Puede crear una recopilación de todos los equipos que no tienen instalado Microsoft Office 2013 y, a continuación, implementar este software en todos los equipos de esa recopilación.<br /><br /> También puede utilizar los requisitos de la aplicación para realizar esta tarea. Para obtener más información, consulte [Cómo crear aplicaciones con System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|Administración de la configuración de clientes|Aunque la configuración predeterminada del cliente de Configuration Manager se aplica a todos los dispositivos y todos los usuarios, puede crear una configuraciones personalizadas de cliente que se apliquen a una recopilación de dispositivos o una recopilación de usuarios.<br /><br /> Por ejemplo, si desea que el control remoto esté disponible en la mayoría de los dispositivos, defina la configuración predeterminada del cliente para permitir el control remoto y, a continuación, defina los parámetros personalizados del cliente que no permiten el control remoto. Implemente esta configuración personalizada del cliente en una recopilación que contenga los equipos que no usarán el control remoto.<br /><br /> Para obtener más información sobre cómo usar recopilaciones para configuraciones de cliente, consulte [About client settings in System Center Configuration Manager (Sobre la configuración de cliente en System Center Configuration Manager)](../../../../core/clients/deploy/about-client-settings.md).|  
|Administración de energía|Para cada recopilación que cree, puede definir la configuración de energía, por ejemplo, el tiempo con que los equipos de la recopilación entran en el modo de suspensión cuando están inactivos.<br /><br /> Para obtener más información sobre cómo usar recopilaciones con la administración de energía, consulte [Introduction to power management (Introducción a la administración de energía)](../power/introduction-to-power-management.md).|  
|Administración basada en roles|Las recopilaciones se pueden usar con la administración basada en roles para controlar qué grupos de usuarios tienen acceso a diversas funcionalidades en la consola de Configuration Manager.<br /><br /> Para obtener más información sobre cómo configurar recopilaciones para la administración basada en roles, consulte [Configurar la administración basada en roles de System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Ventanas de mantenimiento|Las ventanas de mantenimiento proporcionan un medio que los usuarios administrativos pueden emplear para definir un periodo de tiempo durante el cual es posible llevar a cabo varias operaciones de Configuration Manager en miembros de una recopilación de dispositivos. Puede usar las ventanas de mantenimiento para ayudar a garantizar que los cambios en la configuración de cliente se produzcan durante períodos que no afecten la productividad de la organización.<br /><br /> Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo usar ventanas de mantenimiento en System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  

 La mayoría de las tareas de administración se basan en el uso de una o más recopilaciones. Por ejemplo, para poder implementar las actualizaciones de software para dispositivos, debe identificar una recopilación para la implementación de actualizaciones de software. Aunque puede utilizar la recopilación integrada de Todos los sistemas, utilizar esta recopilación para tareas de administración no es una práctica recomendada. Salvo en un entorno de prueba, normalmente se beneficiará de crear sus propias recopilaciones personalizadas para identificar más específicamente los dispositivos o usuarios que va a administrar.  

 Las recopilaciones integradas y personalizadas aparecen en los nodos **Recopilaciones de usuarios** y **Recopilaciones de dispositivos** en el área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager.  

 Las recopilaciones que ha visto recientemente aparecen en el nodo **Usuarios** y en el nodo **Dispositivos** en el área de trabajo **Activos y compatibilidad** en la consola de Configuration Manager.  

## <a name="collection-types-in-configuration-manager"></a>Tipos de recopilación en Configuration Manager  
 Configuration Manager tiene algunas recopilaciones integradas que puede usar para operaciones comunes. Además, puede crear sus propias recopilaciones que agrupen recursos específicos para sus requisitos empresariales.  

### <a name="built-in-collections"></a>Recopilaciones integradas  
 De manera predeterminada, Configuration Manager incluye las siguientes recopilaciones, que no pueden modificarse.  

|**Nombre de recopilación**|Descripción|  
|-------------------------|-----------------|  
|**Todos los grupos de usuarios**|Contiene los grupos de usuarios que se detectan mediante la detección de grupos de seguridad de Active Directory.|  
|**Todos los usuarios**|Contiene los usuarios que se detectan mediante la detección de usuarios de Active Directory.|  
|**Todos los usuarios y grupos de usuarios**|Contiene las recopilaciones Todos los usuarios y Todos los grupos de usuarios. Esta recopilación no se puede modificar y contiene el ámbito más grande de recursos de usuarios y grupos de usuarios.|  
|**Todos los clientes de escritorio y servidor**|Contiene los dispositivos de servidor y de escritorio que tienen instalado el cliente de Configuration Manager. La pertenencia se mantiene mediante la detección de latidos.|  
|**Todos los dispositivos móviles**|Contiene los dispositivos móviles administrados por Configuration Manager. La pertenencia está restringida a aquellos dispositivos móviles que se asignan correctamente a un sitio o los detecta el conector de Exchange Server.|  
|**Todos los sistemas**|Contiene las recopilaciones Todos los clientes de escritorio y servidor, Todos los dispositivos móviles, Todos los equipos desconocidos y todos los dispositivos móviles inscritos por Microsoft Intune.<br /><br /> Esta recopilación no se puede modificar y contiene el ámbito más grande de recursos de dispositivos.|  
|**Todos los equipos desconocidos**|Contiene registros de equipos genéricos para varias plataformas de equipos. Puede utilizar esta recopilación para implementar un sistema operativo mediante una secuencia de tareas y el arranque PXE, medios de arranque o medios preconfigurados.|  

### <a name="custom-collections"></a>Recopilaciones personalizadas  
 Cuando se crea una recopilación personalizada en Configuration Manager, la pertenencia de dicha recopilación viene determinada por una o varias reglas de recopilación. Para obtener información sobre cómo configurar las reglas de recopilación, consulte [Cómo crear recopilaciones en System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). Existen cuatro reglas que puede usar:  

#### <a name="direct-rule"></a>Regla directa  
 Las reglas directas le permiten elegir los usuarios o equipos que quiera agregar como miembros a una recopilación. Esta regla ofrece control directo sobre qué recursos son miembros de la recopilación. Esta pertenencia no cambia automáticamente a menos que se quite un recurso de Configuration Manager. Configuration Manager debe detectar los recursos o se deben importar los recursos antes de poder agregarlos a una recopilación de regla directa. Las recopilaciones de reglas directas tienen una mayor carga administrativa que recopilaciones de reglas de consulta, ya que debe modificar este tipo de recopilación de forma manual.  

#### <a name="query-rule"></a>Regla de consulta  
 Las reglas de consulta actualizan de forma dinámica la pertenencia de una recopilación basándose en una consulta que Configuration Manager ejecuta según una programación. Por ejemplo, puede crear una recopilación de usuarios que sean miembros de la unidad organizativa Recursos humanos de los Servicios de dominio de Active Directory. A diferencia de las recopilaciones de reglas directas, esta pertenencia a la recopilación se actualiza automáticamente cuando se agregan usuarios nuevos o se quitan usuarios de la unidad organizativa Recursos humanos. Las reglas de consulta quitan la sobrecarga administrativa de agregar manualmente los dispositivos a la recopilación mediante una regla directa. Sin embargo, reducen el control que tiene sobre los equipos que se agregan a la recopilación. Entre los ejemplos de reglas basadas en consultas se incluyen:  

-   Todos los usuarios de una UO especificada  

-   Todos los equipos que ejecutan Windows 8  

-   Todos los equipos que tienen más de 20 GB de espacio libre en disco  

#### <a name="include-collections-rule"></a>Regla de inclusión de recopilaciones  
 La regla de inclusión de recopilaciones permite incluir los miembros de otra recopilación en una recopilación de Configuration Manager. Configuration Manager actualiza la pertenencia de la recopilación actual según una programación si cambia la pertenencia de la recopilación incluida.  

#### <a name="exclude-collections-rule"></a>Regla de exclusión de recopilaciones  
 La regla de exclusión de recopilaciones le permite excluir los miembros de otra recopilación de una recopilación de Configuration Manager. Configuration Manager actualiza la pertenencia de la recopilación actual según una programación si cambia la pertenencia de la recopilación excluida.  

> [!NOTE]  
>  Si una recopilación incluye tanto reglas de inclusión de recopilación como reglas de exclusión de recopilación y se produce un conflicto, la regla de exclusión tiene prioridad sobre la regla de inclusión.  

## <a name="incremental-collection-updates"></a>Actualizaciones de recopilación incrementales  
 Cuando habilita las actualizaciones incrementales para una recopilación, Configuration Manager examina periódicamente los recursos nuevos o modificados de la evaluación de recopilación anterior y actualiza una pertenencia a recopilación con estos recursos, independientemente de que se realice una evaluación de recopilación completa. De manera predeterminada, al habilitar las actualizaciones de recopilación incremental, se ejecuta cada 5 minutos y le ayuda a mantener actualizados los datos de la colección sin la sobrecarga de una evaluación de recopilación completa.  

> [!NOTE]  
>  Cuando se crea una nueva recopilación, las actualizaciones incrementales se deshabilitan de forma predeterminada.  



<!--HONumber=Nov16_HO1-->


