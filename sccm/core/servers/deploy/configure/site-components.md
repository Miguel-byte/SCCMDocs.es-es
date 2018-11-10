---
title: Componentes de sitio
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar componentes de sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5ffe1a95252d575a5f828d46932f583f4276c5c0
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411181"
---
# <a name="site-components-for-configuration-manager"></a>Componentes de sitio para Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En cada sitio de Configuration Manager, puede configurar componentes de sitio para modificar el comportamiento de los roles de sistema y los informes de estado de sitio. Las configuraciones de los componentes de sitio se aplican a un sitio y a cada instancia de un rol de sistema de sitio aplicable en el sitio.  

En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione un sitio. En el grupo **Configuración** de la cinta, haga clic en **Configurar componentes de sitio**. Seleccione una de las siguientes opciones:

- [Distribución de software](#software-distribution)  
- [Punto de actualización de software](#software-update-point)  
- [Punto de administración](#management-point)  
- [Notificación de estado](#status-reporting)  
- [Notificación de correo electrónico](#email-notification)
- [Evaluación de pertenencia a recopilación](#bkmk_colleval)


## <a name="about-site-components"></a>Acerca de los componentes de sitio  

 La mayoría de las opciones de los distintos componentes de sitio se explican por sí mismas cuando se ven en la consola de Configuration Manager. Pero la información siguiente puede ayudar a explicar algunas de las configuraciones más complejas, o bien proporcionar contenido adicional.  

> [!Note]  
> Las opciones disponibles para algunos componentes varían con independencia de que se seleccione el sitio de administración central, un sitio primario o un sitio secundario. Algunos componentes no están disponibles para ciertos tipos de sitios.  



### <a name="software-distribution"></a>Distribución de software  

#### <a name="content-distribution-settings"></a>Configuración de distribución de contenido
En la pestaña **General**, se especifican opciones que modifican la manera en que el servidor de sitio transfiere el contenido a sus puntos de distribución. Si aumenta los valores que usa para la configuración de la distribución simultánea, la distribución de contenido puede usar más ancho de banda de red.  

#### <a name="pull-distribution-point"></a>Punto de distribución de extracción
Para más información, vea [Usar un punto de distribución de extracción con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

#### <a name="network-access-account"></a>Cuenta de acceso a la red
Para obtener más información, vea [Cuenta de acceso a la red](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="software-update-point"></a>Punto de actualización de software  

Para obtener más información, consulte [Install a software update point](/sccm/sum/get-started/install-a-software-update-point) (Instalar un punto de actualización de software).  


### <a name="management-point"></a>Punto de administración  

En la pestaña **General**, se configura el sitio para que publique información sobre sus puntos de administración en Active Directory Domain Services.  

Los clientes de Configuration Manager usan puntos de administración para buscar servicios e información de sitio, como la pertenencia al grupo de límites y opciones de selección del certificado PKI. Los clientes también usan puntos de administración para buscar otros puntos de administración en el sitio, así como puntos de distribución desde los que descargar software. Los puntos de administración también ayudan a los clientes a completar la asignación de sitios, y a descargar la directiva de cliente y cargar la información de cliente.  

El método más seguro para que los clientes encuentren puntos de administración consiste en publicarlos en Active Directory Domain Services. Este método de ubicación del servicio requiere que se cumpla lo siguiente:

- El esquema se ha extendido para Configuration Manager.
- Haya un contenedor de **System Management**, con los permisos de seguridad adecuados para que el servidor de sitio publique en este contenedor.
- El sitio de Configuration Manager está configurado para publicar en Active Directory Domain Services.
- Los clientes pertenecen al mismo bosque de Active Directory que el servidor de sitio.  

Si los clientes de la intranet no pueden usar Active Directory Domain Services para encontrar puntos de administración, use la [publicación en DNS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns).  

Para obtener información general sobre la ubicación del servicio, vea [Más información sobre cómo los clientes buscan servicios y recursos de sitio](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publicar puntos de administración seleccionados de intranet en DNS
Especifique esta opción si los clientes de la intranet no pueden encontrar puntos de administración desde Active Directory Domain Services. En su lugar, pueden usar un registro de recursos de ubicación del servicio DNS (SRV RR) para buscar un punto de administración en su sitio asignado.  

Para que Configuration Manager publique puntos de administración de la intranet en DNS, deben cumplirse todas las condiciones siguientes:  

-   Los servidores DNS tienen una versión de BIND que es 8.1.2 o posterior.  

-   Los servidores DNS están configurados para las actualizaciones automáticas y admiten registros de recursos de ubicación del servicio.  

-   Los nombres de dominio completos (FQDN) especificados para los puntos de administración de Configuration Manager tienen entradas de host (registros A o AAA) en DNS.  

> [!WARNING]  
>  Para que los clientes encuentren puntos de administración publicados en DNS, debe asignar los clientes a un sitio específico en lugar de usar la asignación automática de sitios. Configure estos clientes para que usen el código de sitio con el sufijo de dominio de su punto de administración. Para obtener más información, vea [Búsqueda de puntos de administración](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).  

Si los clientes de Configuration Manager no pueden usar Active Directory Domain Services o DNS para buscar puntos de administración en la intranet, usarán [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins). El primer punto de administración que se instala para el sitio se publica de forma automática en WINS cuando se configura para aceptar conexiones de cliente HTTP en la intranet.  


### <a name="status-reporting"></a>Notificación de estado  

Estos valores configuran directamente el nivel de detalle que se incluye en los informes de estado de los sitios y clientes.  


### <a name="email-notification"></a>Notificación de correo electrónico  

Especifique los detalles de la cuenta y del servidor de correo para que Configuration Manager pueda enviar notificaciones de correo de alerta.  

Para obtener más información, consulte [Usar alertas y el sistema de estado](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="bkmk_colleval"></a> Evaluación de pertenencia a recopilación  

Use este componente para establecer la frecuencia con la que se evalúa de forma incremental la pertenencia a una recopilación. La evaluación incremental actualiza la pertenencia a una recopilación solo con recursos nuevos o modificados.  

Para obtener más información, vea [Procedimientos recomendados para recopilaciones](/sccm/core/clients/manage/collections/best-practices-for-collections).



##  <a name="BKMK_ServiceMgr"></a> Usar el Administrador de servicios de Configuration Manager para administrar componentes del sitio  

Puede usar el Administrador de servicios de Configuration Manager para controlar los servicios de Configuration Manager y para ver el estado de los servicios de Configuration Manager o el subproceso de trabajo. Estos servicios y subprocesos se denominan de forma conjunta componentes de Configuration Manager. Es importante que comprenda las afirmaciones siguientes sobre los componentes de Configuration Manager:  

-   Los componentes pueden ejecutarse en cualquier sistema de sitio.  

-   Los componentes se administran de la misma manera que los servicios de Windows. Puede iniciar, detener, pausar, reanudar o consultar componentes de Configuration Manager.  

Un servicio de Configuration Manager se ejecuta cuando hay algo que puede realizar. Normalmente, esta acción es cuando se escribe un archivo de configuración en la Bandeja de entrada de un componente. 


### <a name="use-the-configuration-manager-service-manager"></a>Usar el Administrador de servicios de Configuration Manager  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado del sistema** y haga clic en el nodo **Estado del componente**.  

2.  En el grupo **Componente** de la cinta, haga clic en **Inicio** y, luego, seleccione **Administrador de servicios de Configuration Manager**.  

3.  Cuando se abra el Administrador de servicios de Configuration Manager, conéctese al sitio que desea administrar.  

     Si no ve el sitio que quiere administrar, vaya al menú **Sitio** y haga clic en **Conectar**. Después, escriba el nombre del servidor de sitio del sitio correcto.  

4.  Expanda el sitio y desplácese hasta **Componentes** o **Servidores**, según la ubicación de los componentes que desee administrar.  

5.  En el panel derecho, seleccione uno o más componentes. Después, en el menú **Componente**, haga clic en **Consulta** para actualizar el estado de la selección.  

6.  Una vez se haya actualizado el estado del componente, use una de las cuatro opciones basadas en acciones del menú **Componente** para modificar el funcionamiento del componente. Después de solicitar una acción, debe consultar el componente para mostrar el nuevo estado del componente.  

7.  Cierre el Administrador de servicios de Configuration Manager cuando haya terminado de modificar el estado operativo de los componentes.  
