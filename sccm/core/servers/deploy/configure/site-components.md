---
title: Componentes de sitio para Configuration Manager | Microsoft Docs
description: "Obtenga información sobre cómo configurar componentes de sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En cada sitio de System Center Configuration Manager, puede configurar componentes de sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio. Las configuraciones de los componentes de sitio se aplican a un sitio y a cada instancia de un rol de sistema de sitio aplicable en el sitio.  

## <a name="about-site-components"></a>Acerca de los componentes de sitio  
 La mayoría de las opciones de los distintos componentes de sitio se explican por sí mismas cuando se ven en la consola de Configuration Manager. Aun así, la información siguiente puede ayudar a explicar algunas de las configuraciones más complejas o proporcionar contenido adicional que las explique.  

### <a name="software-distribution"></a>Distribución de software  

-   **Configuración de distribución de contenido:** puede especificar opciones que modifiquen la manera en que el servidor de sitio transfiere el contenido a los puntos de distribución. Si aumenta los valores que usa para la configuración de la distribución simultánea, la distribución de contenido puede usar más ancho de banda de red.  

-   **Cuenta de acceso a la red:** para obtener información sobre la configuración y el uso de la cuenta de acceso a la red, vea [Cuenta de acceso a la red](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Punto de actualización de software  

-   Para obtener información sobre las opciones de configuración del componente de punto de actualización de software, vea [Instalar y configurar un punto de actualización de software](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Punto de administración  

-   **Puntos de administración:** puede configurar el sitio para que publique información sobre sus puntos de administración en Active Directory Domain Services.  

     Los clientes de Configuration Manager usan puntos de administración para buscar servicios e información de sitio, como la pertenencia al grupo de límites y opciones de selección del certificado PKI. Los clientes también usan puntos de administración para buscar otros puntos de administración en el sitio, así como puntos de distribución desde los que descargar software. Los puntos de administración también ayudan a los clientes a completar la asignación de sitios, y a descargar la directiva de cliente y cargar la información de cliente.  

     Como el método más seguro de buscar puntos de administración para los clientes es publicarlos en Active Directory Domain Services, siempre se suelen seleccionar todos los puntos de administración que funcionan para publicarlos en Active Directory Domain Services. En cambio, este método de ubicación del servicio requiere que se cumplan las condiciones siguientes:

     - El esquema se ha extendido para Configuration Manager.
     - Hay un contenedor de **System Management** con permisos de seguridad adecuados para que el servidor de sitio publique en este contenedor.
     - El sitio de Configuration Manager está configurado para publicar en Active Directory Domain Services.
     - Los clientes pertenecen al mismo bosque de Active Directory que el servidor de sitio.  

     Si los clientes de la intranet no pueden usar Active Directory Domain Services para encontrar puntos de administración, use la publicación en [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

 Para obtener información general sobre la ubicación del servicio, consulte [Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar puntos de administración de intranet seleccionados en DNS:** especifique esta opción cuando los clientes de la intranet no pueden encontrar puntos de administración de Active Directory Domain Services. En su lugar, pueden usar un registro de recursos de ubicación del servicio DNS (SRV RR) para buscar un punto de administración en su sitio asignado.  

    Para que Configuration Manager publique puntos de administración de la intranet en DNS, deben cumplirse todas las condiciones siguientes:  

    -   Los servidores DNS tienen una versión de BIND que es 8.1.2 o posterior.  

    -   Los servidores DNS están configurados para las actualizaciones automáticas y admiten registros de recursos de ubicación del servicio.  

    -   Los nombres de dominio completos (FQDN) especificados para los puntos de administración de Configuration Manager tienen entradas de host (registros A o AAA) en DNS.  

    > [!WARNING]  
    >  Para que los clientes encuentren puntos de administración publicados en DNS, debe asignar los clientes a un sitio específico en lugar de usar la asignación automática de sitios. Configure estos clientes para que usen el código de sitio con el sufijo de dominio de su punto de administración. Para obtener más información, vea [Búsqueda de puntos de administración](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) en [Cómo asignar clientes a un sitio en System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Si los clientes de Configuration Manager no pueden usar Active Directory Domain Services o DNS para buscar puntos de administración en la intranet, usarán [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). El primer punto de administración que se instala para el sitio se publica automáticamente en WINS cuando se configura para aceptar conexiones de cliente HTTP en la intranet.  

### <a name="status-reporting"></a>Notificación de estado  

-   Estos valores configuran directamente el nivel de detalle que se incluye en los informes de estado de los sitios y clientes.  

### <a name="email-notification"></a>Notificación de correo electrónico  

-   Especifique los detalles de la cuenta y del servidor de correo para que Configuration Manager pueda enviar notificaciones de correo de alerta.  

### <a name="collection-membership-evaluation"></a>Evaluación de pertenencia a recopilación  

-   Use esta tarea para establecer la frecuencia con la que se evalúa incrementalmente la pertenencia a una recopilación. La evaluación incremental actualiza la pertenencia a una recopilación solo con recursos nuevos o modificados.  

### <a name="edit-the-site-components-at-a-site"></a>Modificar los componentes de un sitio  

Siga estos pasos para modificar los componentes de un sitio:

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de sitio** > **Sitios** y, después, seleccione el sitio que tenga los componentes de sitio que quiere configurar.  

2.  En la pestaña **Inicio**, en el grupo **Configuración**, haga clic en **Configurar componentes de sitio**. Después, seleccione el componente de sitio que quiere configurar.  

##  <a name="BKMK_ServiceMgr"></a> Usar el Administrador de servicios de Configuration Manager para administrar componentes del sitio  
Puede usar el Administrador de servicios de Configuration Manager para controlar los servicios de Configuration Manager y para ver el estado de los servicios de Configuration Manager o el subproceso de trabajo (denominados de forma conjunta componentes de Configuration Manager). Es importante que comprenda lo siguiente sobre los componentes de Configuration Manager:  

-   Los componentes pueden ejecutarse en cualquier sistema de sitio.  

-   Los componentes se administran de la misma manera que los servicios de Windows. Puede iniciar, detener, pausar, reanudar o consultar componentes de Configuration Manager.  

Un servicio de Configuration Manager se ejecuta cuando tiene asignada una tarea (normalmente, cuando un archivo de configuración se escribe en la bandeja de entrada de un componente). Si es necesario identificar el componente implicado en una operación, puede usar el Administrador de servicios de Configuration Manager para manipular varios servicios y subprocesos. Después, puede ver el cambio resultante en el comportamiento de Configuration Manager. Por ejemplo, puede detener servicios de Configuration Manager de uno en uno hasta que se elimine una respuesta determinada. De este modo puede determinar qué servicio causa ese comportamiento.  

> [!TIP]  
>  El siguiente procedimiento puede usarse para manipular operaciones de componentes de Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Usar el Administrador de servicios de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión** >  **Estado del sistema** y luego haga clic en **Estado del componente**.  

2.  En la pestaña **Inicio**, en el grupo **Componente**, haga clic en **Iniciar**. Después, seleccione **Administrador de servicios de Configuration Manager**.  

3.  Cuando se abra el Administrador de servicios de Configuration Manager, conéctese al sitio que desea administrar.  

     Si no ve el sitio que desea administrar, haga clic en **Sitio**, haga clic en **Conectar**y, a continuación, escriba el nombre del servidor de sitio del sitio correcto.  

4.  Expanda el sitio y desplácese hasta **Componentes** o **Servidores**, según la ubicación de los componentes que desee administrar.  

5.  En el panel derecho, seleccione uno o más componentes. Después, en el menú **Componente**, haga clic en **Consulta** para actualizar el estado de la selección.  

6.  Una vez se haya actualizado el estado del componente, use una de las cuatro opciones basadas en acciones del menú **Componente** para modificar el funcionamiento del componente. Después de solicitar una acción, debe consultar el componente para mostrar el nuevo estado del componente.  

7.  Cierre Configuration Manager Service Manager cuando haya terminado de modificar el estado operativo de los componentes.  
