---
title: Componentes de sitio | System Center Configuration Manager
description: "Obtenga información sobre cómo configurar componentes de sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a0c2ff2ad2f76e7e769d49674ccf4d3efe6b4f3e


---
# <a name="site-components-for-system-center-configuration-manager"></a>Componentes de sitio para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En cada sitio de System Center Configuration Manager, puede configurar componentes de sitio para modificar el comportamiento de los roles de sistema de sitio y los informes de estado de sitio. Las configuraciones de los componentes de sitio se aplican a un sitio y a cada instancia de un rol de sistema de sitio aplicable en el sitio.  

## <a name="about-site-components"></a>Acerca de los componentes de sitio  
 La mayoría de las opciones de los distintos componentes de sitio se explican por sí mismas cuando se ven en la consola de Configuration Manager. Sin embargo, la información siguiente puede ayudar a explicar algunas de las configuraciones más complejas o a proporcionar contenido adicional que las explica:  

**Distribución de software:**  

-   **Configuración de distribución de contenido:**  puede configurar opciones que modifiquen la manera en que el servidor de sitio transfiere el contenido a los puntos de distribución. Si aumenta los valores que usa para la configuración de la distribución simultánea, la distribución de contenido puede usar más ancho de banda de red.  

-   **Cuenta de acceso a la red:** para obtener información sobre la configuración y el uso de la cuenta de acceso a la red, consulte [Network Access Account](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) (Cuenta de acceso a la red)  

**Punto de actualización de software:**  

-   Para obtener información sobre las opciones de configuración del componente de punto de actualización de software, consulte [Install and configure a software update point](../../../../sum/get-started/install-a-software-update-point.md) (Instalar y configurar un punto de actualización de software).  

**Punto de administración:**  

-   **Puntos de administración:** puede configurar el sitio para que publique información sobre sus puntos de administración en Servicios de dominio de Active Directory.  

     Los clientes de Configuration Manager usan puntos de administración para la ubicación del servicio, para buscar información de sitio como opciones de pertenencia a un grupo delimitador y de selección de certificados PKI, así como para buscar otros puntos de administración del sitio y puntos de distribución desde los que descargar software. Los clientes también utilizan puntos de administración para completar la asignación de sitios, descargar la directiva de cliente y cargar la información de cliente.  

     Como el método más seguro de buscar puntos de administración para los clientes es publicarlos en Active Directory Domain Services, siempre se suelen seleccionar todos los puntos de administración que funcionan para publicarlos en Active Directory Domain Services. En cambio, este método de ubicación del servicio requiere que el esquema se amplíe para Configuration Manager, que haya un contenedor **System Management** con los permisos de seguridad adecuados para que el servidor de sitio publique en este contenedor, que el sitio de Configuration Manager esté configurado para publicar en Active Directory Domain Services y que los clientes formen parte del mismo bosque de Active Directory que el bosque del servidor de sitio.  

     Si los clientes de la intranet no pueden usar Active Directory Domain Services para encontrar puntos de administración, use la publicación en [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns).  

     Para obtener información general sobre la ubicación del servicio, consulte [Comprender cómo los clientes buscan servicios y recursos de sitio para System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publicar puntos de administración de intranet seleccionados en DNS:** especifique esta opción si los clientes de la intranet no pueden encontrar puntos de administración desde Servicios de dominio de Active Directory, pero pueden usar un registro de recursos de ubicación de servicio DNS (SRV RR) para encontrar puntos de administración en su sitio asignado.  

    Para que Configuration Manager publique puntos de administración de la intranet en DNS, deben cumplirse todas las condiciones siguientes:  

    -   Los servidores DNS tienen una versión de BIND que es 8.1.2 o posterior.  

    -   Los servidores DNS están configurados para las actualizaciones automáticas y admiten registros de recursos de ubicación del servicio.  

    -   Los FQDN especificados para los puntos de administración de Configuration Manager tienen entradas de host (registros A o AAA) en DNS.  

    > [!WARNING]  
    >  Para que los clientes encuentren puntos de administración publicados en DNS, debe asignar los clientes a un sitio específico, en vez de usar la asignación automática de sitio, y configurar los clientes para que usen el código de sitio con el sufijo de dominio de su punto de administración. Para obtener más información, consulte [Búsqueda de puntos de administración](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_LocatingMPs) en [Cómo asignar clientes a un sitio en System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

     Si los clientes de Configuration Manager usan Active Directory Domain Services o DNS para encontrar puntos de administración en la intranet, pasarán a usar [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). El primer punto de administración que se instala para el sitio se publica automáticamente en WINS cuando se configura para aceptar conexiones de cliente HTTP en la intranet.  

**Notificación de estado:**  

-   Estos valores configuran directamente el nivel de detalle que se incluye en los informes de estado de los sitios y clientes.  

**Notificación de correo electrónico:**  

-   Especifique los detalles de la cuenta y del servidor de correo para que Configuration Manager pueda enviar notificaciones de correo de alerta.  

**Evaluación de pertenencia a recopilación:**  

-   Use esta tarea para establecer la frecuencia con la que se evalúa incrementalmente la pertenencia a una recopilación. La evaluación incremental actualiza la pertenencia a una recopilación solo con recursos nuevos o modificados.  

#### <a name="to-edit-the-site-components-at-a-site"></a>Para modificar los componentes de un sitio  

1.  En la consola de Configuration Manager, haga clic en **Administración** > **Configuración de sitio** > **Sitios** y después seleccione el sitio que tiene los componentes de sitio que va a configurar.  

2.  En la pestaña **Inicio** , en el grupo **Configuración** , haga clic en **Configurar componentes de sitio** y, a continuación, en el componente de sitio que desea configurar.  

##  <a name="a-namebkmkservicemgra-use-the-configuration-manager-service-manager-to-manage-site-components"></a><a name="BKMK_ServiceMgr"></a> Usar el Administrador de servicios de Configuration Manager para administrar componentes del sitio  
Puede usar Configuration Manager Service Manager para controlar los servicios de Configuration Manager y para ver el estado de los servicios de Configuration Manager o el subproceso de trabajo (denominados de forma conjunta componentes de Configuration Manager):  

-   Los componentes de Configuration Manager pueden ejecutarse en cualquier sistema de sitio.  

-   Los componentes se administran de la misma manera que se administran los servicios en Windows; es posible iniciar, detener, pausar, reanudar o consultar componentes de Configuration Manager.  

Un servicio de Configuration Manager se ejecuta cuando tiene asignada una tarea (normalmente, cuando un archivo de configuración se escribe en la bandeja de entrada de un componente). Si es necesario identificar el componente involucrado en una operación, puede usar **Configuration Manager Service Manager** para manipular varios servicios y subprocesos de Configuration Manager y después ver el cambio resultante en el comportamiento de Configuration Manager. Por ejemplo, puede detener servicios de Configuration Manager de uno en uno hasta que se elimine una respuesta determinada. De este modo puede determinar qué servicio causa ese comportamiento.  

> [!TIP]  
>  El siguiente procedimiento puede usarse para manipular operaciones de componentes de Configuration Manager.  

#### <a name="to-use-the-configuration-manager-service-manager"></a>Para utilizar el Administrador de servicios de Configuration Manager  

1.  En la consola de Configuration Manager, haga clic en **Supervisión** >  **Estado del sistema** y luego haga clic en **Estado del componente**.  

2.  En la pestaña **Inicio** , en el grupo **Componente** , haga clic en **Inicio**y, a continuación, seleccione **Administración de servicios de Configuration Manager**.  

3.  Cuando se abra el Administrador de servicios de Configuration Manager, conéctese al sitio que desea administrar.  

     Si no ve el sitio que desea administrar, haga clic en **Sitio**, haga clic en **Conectar**y, a continuación, escriba el nombre del servidor de sitio del sitio correcto.  

4.  Expanda el sitio y desplácese hasta **Componentes** o **Servidores** dependiendo de la ubicación de los componentes que desee administrar.  

5.  En el panel derecho, seleccione uno o más componentes y, a continuación, en el menú **Componente** , haga clic en **Consulta** para actualizar el estado de la selección.  

6.  Una vez se haya actualizado el estado del componente, use una de las cuatro opciones basadas en acciones del menú **Componente** para modificar las operaciones de componentes. Después de solicitar una acción, debe consultar el componente para mostrar el nuevo estado del componente.  

7.  Cierre Configuration Manager Service Manager cuando haya terminado de modificar el estado operativo de los componentes.  



<!--HONumber=Nov16_HO1-->


