---
title: Alta disponibilidad
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo implementar System Center Configuration Manager mediante el uso de opciones que mantienen un alto nivel de servicio disponible.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1011aa1b30661d756d457a38ebc770a61fac07f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Opciones de alta disponibilidad para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*



Puede implementar System Center Configuration Manager mediante el uso de opciones que mantienen un alto nivel de servicio disponible.   

Opciones que admiten la alta disponibilidad:   

-   Los sitios admiten varias instancias de servidores de sistema de sitio que ofrecen servicios importantes a los clientes.  

-   Los sitios de administración central y los sitios primarios admiten la copia de seguridad de la base de datos del sitio. La base de datos del sitio contiene todas las configuraciones de sitios y clientes, y se comparte entre los sitios de una jerarquía que contiene un sitio de administración central.  

-   Las opciones de recuperación de sitio integrada pueden reducir el tiempo de inactividad del servidor e incluyen opciones avanzadas que simplifican la recuperación cuando tiene una jerarquía con un sitio de administración central.  

-   Los clientes pueden corregir automáticamente los problemas más frecuentes sin intervención administrativa.  

-   Los sitios generan alertas acerca de los clientes que no pueden enviar datos recientes, lo que alerta a los administradores sobre posibles problemas.  

-   Configuration Manager proporciona varios informes integrados que le permiten identificar problemas y tendencias antes de que se conviertan en problemas para las operaciones del cliente o el servidor.  

 Configuration Manager no proporciona un servicio en tiempo real y debe esperar que funcione con cierta latencia de datos. Por lo tanto, es poco común en la mayoría de escenarios que implican una interrupción temporal del servicio que se conviertan en un problema crítico. Cuando haya configurado sus sitios y jerarquías con alta disponibilidad en mente, se puede minimizar el tiempo de inactividad, mantener la autonomía de las operaciones y proporcionar un alto nivel de servicio.  

 Por ejemplo, los clientes de Configuration Manager suelen funcionar de forma autónoma mediante el uso de programaciones y configuraciones conocidas de operaciones, y programaciones para enviar datos al sitio para su procesamiento.  

-   Cuando los clientes no pueden ponerse en contacto con el sitio, almacenan en caché los datos que desean enviar hasta que pueden ponerse en contacto con el sitio.  

-   Los clientes que no pueden ponerse en contacto con el sitio siguen funcionando con las últimas programaciones conocidas y la información almacenada en caché, como una aplicación descargada previamente que deben ejecutar o instalar, hasta que pueden ponerse en contacto con el sitio y recibir nuevas directivas.  

-   El sitio supervisa sus sistemas de sitio y clientes para obtener actualizaciones de estado periódicas, y puede generar alertas cuando estas no se registren.  

-   Los informes integrados proporcionan información sobre las operaciones en curso, así como operaciones históricas y tendencias. Configuration Manager también admite mensajes basados en el estado que proporcionan información casi en tiempo real de las operaciones en curso.  

  Utilice la información de este tema con la información de los siguientes artículos:
-   [Hardware recomendado](../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemas operativos compatibles para los servidores de sistema de sitio](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Requisitos previos de sitio y sistema de sitio](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a> Alta disponibilidad de sitios y jerarquías  
 **Usar un clúster de SQL Server para hospedar la base de datos del sitio:**  

 Cuando se utiliza un clúster de SQL Server para la base de datos en un sitio de administración central o un sitio primario, se utiliza la compatibilidad con la conmutación por error integrada en SQL Server.  

 Los sitios secundarios no pueden utilizar un clúster de SQL Server y no son compatibles con la copia de seguridad o restauración de la base de datos del sitio. Recupere un sitio secundario volviendo a instalarlo desde su sitio primario principal.  

 **Usar un grupo de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos del sitio:**  

 A partir de la versión 1602, puede usar grupos de disponibilidad AlwaysOn de SQL Server para hospedar la base de datos del sitio en sitios primarios y el sitio de administración central como una solución de alta disponibilidad y recuperación ante desastres. Para obtener más información, consulte [SQL Server AlwaysOn para una base de datos de sitio de alta disponibilidad para System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Implementar una jerarquía de sitios con un sitio de administración central y uno o varios sitios primarios secundarios:**  

 Esta configuración puede proporcionar tolerancia a errores cuando los sitios administran segmentos de la red que se superponen. Además, esta configuración ofrece una opción de recuperación adicional para usar la información en la base de datos compartida disponible en otro sitio, para volver a crear la base de datos del sitio en el sitio recuperado. Puede usar esta opción para reemplazar una copia de seguridad con errores o no disponible de la base de datos del sitio con errores.  

 **Crear copias de seguridad periódicas en sitios de administración central y sitios primarios:**  

 Cuando cree y pruebe una copia de seguridad de sitio periódica, puede asegurarse de que tiene los datos necesarios para recuperar un sitio y la experiencia para recuperar un sitio en la mínima cantidad de tiempo posible.  

 **Instalar varias instancias de roles de sistema de sitio:**  

 Cuando instale varias instancias de roles de sistema de sitio críticos, como el punto de administración o el punto de distribución, proporcione puntos de contacto redundantes para los clientes en caso de que un servidor de sistema de sitio específico se quede sin conexión.  

 **Instalar varias instancias del proveedor de SMS en un sitio:** el proveedor de SMS proporciona el punto de contacto administrativo para una o más consolas de Configuration Manager. Al instalar varios proveedores de SMS, puede proporcionar redundancia a los puntos de contacto para administrar el sitio y la jerarquía.  

##  <a name="bkmk_ssr"></a> Alta disponibilidad para los roles de sistema de sitio  
 En cada sitio, se implementan roles de sistema de sitio para proporcionar los servicios que desea que los clientes utilicen en ese sitio. La base de datos del sitio contiene la información de configuración del sitio y de todos los clientes. Utilice una o varias de las opciones disponibles para proporcionar alta disponibilidad de la base de datos del sitio y la recuperación del sitio y de la base de datos de sitio si es necesario.  

 **Redundancia de roles de sistema de sitio importantes:**  

-   Punto de servicio web del catálogo de aplicaciones  

-   Punto de sitios web del catálogo de aplicaciones  

-   Punto de distribución  

-   Punto de administración  

-   Punto de actualización de software  

-   Punto de migración de estado  

 Puede instalar varias instancias del rol de punto de servicios de informes para proporcionar redundancia de informes en sitios y clientes.

 Puede usar PowerShell para instalar el rol de sistema de sitio del punto de actualización de software en un clúster de equilibrio de carga de red (NLB) de Windows a fin de proporcionar compatibilidad con la conmutación por error.  


 **Copia de seguridad de sitio integrada:**  

 Configuration Manager incluye una tarea de copia de seguridad integrada para ayudarle a crear una copia de seguridad de su sitio y de la información crítica según una programación periódica. Además, el Asistente para instalación de Configurarion Manager admite acciones de restauración del sitio para ayudarle a restaurar un sitio para que funcione de nuevo.  

 **Publicación en Active Directory Domain Services y DNS:**  

 Puede configurar cada sitio para publicar datos acerca de servidores de sistema de sitio y servicios en Active Directory Domain Services y DNS. Esto permite a los clientes identificar el servidor más accesible de la red e identificar cuándo están disponibles los nuevos servidores de sistema de sitio que pueden proporcionar servicios importantes, como puntos de administración.  

 **Proveedor de SMS y consola de Configuration Manager:**  

 Configuration Manager admite la instalación de varios proveedores de SMS, cada uno en un equipo diferente, para asegurar varios puntos de acceso para la consola de Configuration Manager. Esto garantiza que si un equipo de proveedor de SMS está desconectado, se mantiene la posibilidad de ver y volver a configurar sitios y clientes de Configuration Manager.  

 Cuando una consola de Configuration Manager se conecta a un sitio, se conecta a una instancia del proveedor de SMS en ese sitio. La instancia del proveedor de SMS se selecciona de forma no determinista. Si el proveedor de SMS seleccionado no está disponible, tiene las siguientes opciones:  

-   Vuelva a conectar la consola al sitio. Cada nueva solicitud de conexión se asigna de forma no determinista a una instancia del proveedor de SMS y es posible que la nueva conexión se asigne a una instancia disponible.  

-   Conecte la consola a otro sitio de Configuration Manager y administre la configuración desde esa conexión. Esto presenta un ligero retraso de los cambios de configuración de no más de unos minutos. Una vez que el proveedor de SMS para el sitio esté conectado, puede volver a conectar su consola de Configuration Manager directamente al sitio que desee administrar.  

 Puede instalar la consola de Configuration Manager en varios equipos para que la usen los usuarios administrativos. Cada proveedor de SMS admite conexiones procedentes de varias consolas de Configuration Manager.  

 **Punto de administración:**  

 Instale varios puntos de administración en cada sitio primario y habilite los sitios para publicar datos del sitio en su infraestructura de Active Directory y en DNS.  

 Varios puntos de administración ayudan a equilibrar la carga del uso de cualquier punto de administración único por parte de varios clientes. Además, puede instalar una o varias réplicas de base de datos de puntos de administración para reducir las operaciones de uso intensivo de la CPU del punto de administración y aumentar la disponibilidad de este rol de sistema de sitio crítico.  

 Debido a que solo puede instalar un punto de administración en un sitio secundario, que debe estar ubicado en un servidor de sitio secundario, no se considera que los puntos de administración en sitios secundarios tengan una configuración de alta disponibilidad.  

> [!NOTE]  
>  Los dispositivos administrados mediante la administración de dispositivos móviles local se conectan a un único punto de administración en un sitio primario. Configuration Manager asigna el punto de administración al dispositivo móvil durante la inscripción y, después, no cambia. Al instalar varios puntos de administración y habilitar más de uno para dispositivos móviles, el punto de administración que se asigna a un cliente de dispositivo móvil no es determinista.  
>   
>  Si el punto de administración que usa un cliente de dispositivo móvil deja de estar disponible, debe resolver el problema con este punto de administración o borrar el dispositivo móvil y volver a inscribirlo de forma que pueda asignarse a un punto de administración operativa habilitado para dispositivos móviles.  

 **Punto de distribución:**  

 Instale varios puntos de distribución y distribuya contenido a varios puntos de distribución. Puede configurar grupos de límites superpuestos para la ubicación de contenido para asegurarse de que los clientes de cada subred pueden tener acceso a una implementación desde dos o más puntos de distribución. Por último, es recomendable configurar uno o más puntos de distribución como ubicaciones de reserva para el contenido.  

 Para obtener más información sobre la reserva de ubicaciones de contenido, consulte [Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Punto de servicio web del catálogo de aplicaciones y punto de sitios web del catálogo de aplicaciones:**  

 Puede instalar varias instancias de cada rol de sistema de sitio y, para conseguir el mejor rendimiento, implementar uno de cada en el mismo equipo de sistema de sitio.  

 Cada rol de sistema de sitio de catálogo de aplicaciones proporciona la misma información que las otras instancias del rol de sistema de sitio independientemente de la ubicación del rol de servidor de sitio en la jerarquía. Por lo tanto, si un cliente realiza una solicitud del catálogo de aplicaciones y ha configurado la opción de cliente de dispositivo Punto de sitios web del catálogo de aplicaciones predeterminado como Detectar automáticamente, el cliente puede ser dirigido a una instancia disponible. Se da preferencia a los servidores locales de sistema de sitio de catálogo de aplicaciones, en función de la ubicación de red actual del cliente.  

 Para obtener más información sobre esta configuración de cliente y el funcionamiento de la detección automática, consulte la sección [Agente de equipo](../../core/clients/deploy/about-client-settings.md#computer-agent) del tema [About client settings in System Center Configuration Manager (Sobre la configuración de cliente en System Center Configuration Manager)](../../core/clients/deploy/about-client-settings.md).  

##  <a name="bkmk_client"></a> Alta disponibilidad para clientes  
 **Las operaciones de cliente son autónomas:**  

 La autonomía del cliente de Configuration Manager incluye lo siguiente:  

-   Los clientes no requieren un contacto continuo con ningún servidor de sistema de sitio específico. Usan configuraciones conocidas para realizar acciones preconfiguradas según una programación.  

-   Los clientes pueden usar cualquier instancia disponible de un rol de sistema de sitio que proporcione servicios a los clientes e intentarán ponerse en contacto con servidores conocidos hasta que se encuentre un servidor disponible.  

-   Los clientes pueden ejecutar inventario, implementaciones de software y acciones programadas similares independientemente del contacto directo con los servidores de sistema de sitio.  

-   Los clientes que están configurados para utilizar un punto de estado de reserva pueden enviar detalles al punto de estado de reserva cuando no se pueden comunicar con un punto de administración.  

 **Los clientes pueden repararse a sí mismos:**  

 Los clientes corrigen automáticamente los problemas más comunes sin intervención administrativa directa:  

-   Periódicamente, los clientes autoevalúan su estado y toman medidas para remediar los problemas más habituales mediante el uso de una caché local que almacena pasos de corrección y archivos de origen para realizar reparaciones.  

-   Cuando un cliente no puede enviar información de estado a su sitio, el sitio puede generar una alerta. Los usuarios administrativos que reciban estas alertas pueden emprender acciones inmediatas para restaurar el funcionamiento normal del cliente.  

 **Los clientes almacenan en caché información para usarla en el futuro:**  

 Cuando un cliente se comunica con un punto de administración, puede obtener y almacenar en caché la información siguiente:  

-   Configuración de cliente.  

-   Programaciones de cliente.  

-   Información acerca de las implementaciones de software y una descarga del software que el cliente está programado para instalar, cuando la implementación está configurada para realizar esta acción.  

 Cuando un cliente no puede ponerse en contacto con un punto de administración, los clientes almacenan en memoria caché local el estado y la información del cliente que envían al sitio, y transfieren estos datos una vez que establecen contacto con un punto de administración.  

 **El cliente puede enviar el estado a un punto de estado de reserva:**  

 Cuando se configura un cliente para que use un punto de estado de reserva, se proporciona un punto adicional de contacto para que el cliente pueda enviar detalles importantes sobre su funcionamiento. Los clientes configurados para usar un punto de estado de reserva siguen enviando el estado de sus operaciones al rol de sistema de sitio, incluso cuando el cliente no se puede comunicar con un punto de administración.  

 **Administración central de los datos del cliente y la identidad del cliente:**  

 La base de datos del sitio, en lugar del cliente individual, conserva información importante sobre la identidad de cada cliente y asocia esos datos a un equipo específico o usuario. Esto significa que:  

-   Los archivos de origen de cliente en un equipo se pueden desinstalar y volver a instalar sin que afecte a los registros históricos del equipo donde está instalado el cliente.  

-   Un error en un equipo cliente no afecta a la integridad de la información almacenada en la base de datos. Esta información puede estar disponible en los informes.  

##  <a name="bkmk_nonHAoptions"></a> Opciones de sitios y roles de sistema de sitio que no tienen una alta disponibilidad  
 Varios sistemas de sitio no admiten distintas instancias en un sitio o en la jerarquía. Esta información puede ayudarle a prepararse para cuando estos sistemas de sitio se desconecten.  

 **Servidor de sitio (sitio):**  

 Configuration Manager no admite la instalación del servidor de sitio para cada sitio en un clúster de Windows Server o NLB.  

 La información siguiente le permite prepararse para situaciones en las que se produce un error de un servidor de sitio o el servidor de sitio no está operativo:  

-   Utilice la tarea de copia de seguridad integrada para crear con regularidad una copia de seguridad del sitio. En un entorno de prueba, practique con regularidad la restauración de sitios mediante una copia de seguridad.  

-   Implemente varios sitios primarios de Configuration Manager en una jerarquía con un sitio de administración central para crear redundancia. Si experimenta un error de sitio, considere la posibilidad de usar scripts de inicio de sesión o directivas de grupo de Windows para reasignar los clientes a un sitio operativo.  

-   Si tiene una jerarquía con un sitio de administración central, puede recuperar el sitio de administración central o el sitio primario secundario mediante la opción de recuperación de una base de datos del sitio de otro sitio en su jerarquía.  

-   Los sitios secundarios no se pueden restaurar y deben volver a instalarse.  

 **Punto de sincronización de Asset Intelligence (jerarquía):**  

 Este rol de sistema de sitio no es crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

-   Resuelva la causa de la desconexión del sistema de sitio.  

-   Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

 **Punto de Endpoint Protection (jerarquía):**  

 Este rol de sistema de sitio no es crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

-   Resuelva la causa de la desconexión del sistema de sitio.  

-   Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

 **Punto de inscripción (sitio):**  

 Este rol de sistema de sitio no es crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

-   Resuelva la causa de la desconexión del sistema de sitio.  

-   Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

 **Punto de proxy de inscripción (sitio):**  

 Este rol de sistema de sitio no es crítico y ofrece una funcionalidad opcional en Configuration Manager. Sin embargo, puede instalar varias instancias de este rol de sistema de sitio en un sitio y en varios sitios en la jerarquía. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

-   Resuelva la causa de la desconexión del sistema de sitio.  

-   Desinstale el rol del servidor actual e instale el rol en un nuevo servidor.  

 Si hay más de un servidor proxy de inscripción en un sitio, utilice un alias DNS para el nombre del servidor. Si utiliza esta configuración, el round robin de DNS proporciona cierta tolerancia a errores y equilibrio de carga cuando los usuarios inscriben sus dispositivos móviles.  

 **Punto de estado de reserva (sitio o jerarquía):**  

 Este rol de sistema de sitio no es crítico y ofrece una funcionalidad opcional en Configuration Manager. Si este sistema de sitio se desconecta, utilice una de las opciones siguientes:  

-   Resuelva la causa de la desconexión del sistema de sitio.  

-   Desinstale el rol del servidor actual e instale el rol en un nuevo servidor. Dado que el punto de estado de reserva se asigna a los clientes durante la instalación de cliente, debe modificar los clientes existentes para utilizar el nuevo servidor de sistema de sitio.  

### <a name="see-also"></a>Consulte también  
 [Configuraciones admitidas para System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)
