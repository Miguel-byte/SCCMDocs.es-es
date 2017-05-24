---
title: "Planificación de Cloud Management Gateway | Microsoft Docs"
description: 
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ae60eb25383f4bd07faaa1265185a471ee79b1e9
ms.openlocfilehash: b1295891a5567e64b901c79100c2971e526dc874
ms.contentlocale: es-es
ms.lasthandoff: 05/17/2017

---

# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planificación de Cloud Management Gateway en Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

A partir de la versión 1610, la puerta de enlace de administración en la nube proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. El servicio de puerta de enlace de administración en la nube se implementa en Microsoft Azure y requiere una suscripción de Azure. Se conecta a la infraestructura de Configuration Manager local con un nuevo rol denominado punto de conexión de la puerta de enlace de administración en la nube. Una vez implementado y configurado, los clientes podrán tener acceso a los roles de sistema de sitio locales de Configuration Manager independientemente de si están conectados a la red interna privada o a Internet.

Use la consola de Configuration Manager para implementar el servicio en Azure, agregar el rol de punto de conexión de la puerta de enlace de administración en la nube y configurar roles de sistema de sitio para permitir el tráfico de la puerta de enlace de administración en la nube. La puerta de enlace de administración en la nube de momento solo admite los roles de punto de administración y punto de actualización de software.

Se necesitan certificados de cliente y de capa de sockets seguros (SSL) para autenticar los equipos y cifrar las comunicaciones entre los diferentes niveles del servicio. Los equipos cliente normalmente reciben un certificado de cliente mediante la aplicación de directivas de grupo. Para cifrar el tráfico entre los clientes y el servidor de sistema de sitio que hospeda los roles, tiene que crear un certificado SSL personalizado de la CA. También debe configurar un certificado de administración en Azure que permita a Configuration Manager implementar el servicio de puerta de enlace de administración en la nube.

## <a name="requirements-for-cloud-management-gateway"></a>Requisitos para la puerta de enlace de administración en la nube

-   Equipos cliente y servidor de sistema de sitio que ejecuten el punto de conexión de la puerta de enlace de administración en la nube.

-   Certificados SSL personalizados de la CA interna: se usan para cifrar la comunicación de los equipos cliente y para autenticar la identidad del servicio de puerta de enlace de administración en la nube.

-   Suscripción de Azure para los servicios en la nube.

-   Certificado de administración de Azure: se usa para autenticar Configuration Manager con Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Especificaciones para la puerta de enlace de administración en la nube

- Cada instancia de puerta de enlace de administración en la nube admite 4000 clientes.
- Se recomienda que cree al menos dos instancias de puerta de enlace de administración en la nube para mejorar la disponibilidad.
- La puerta de enlace de administración en la nube solo admite los roles de punto de administración y punto de actualización de software.
-   En estos momentos, las siguientes características de Configuration Manager no son compatibles con la puerta de enlace de administración en la nube:

    -   Implementación de cliente
    -   Asignación automática de sitio
    -   Directivas de usuario
    -   Catálogo de aplicaciones (incluidas las solicitudes de aprobación de software)
    -   Implementación completa de sistema operativo (OSD)
    -   Consola de Configuration Manager
    -   Herramientas remotas
    -   Sitio web de generación de informes
    -   Wake on LAN
    -   Clientes Mac, Linux y UNIX
    -   Azure Resource Manager
    -   Almacenamiento en caché del mismo nivel
    -   Administración local de dispositivos móviles

## <a name="cost-of-cloud-management-gateway"></a>Costo de la puerta de enlace de administración en la nube

>[!IMPORTANT]
>La información de costo que se proporciona a continuación se indica solo con fines de estimación. Su entorno puede tener otras variables que afecten al costo general del uso de la puerta de enlace de administración en la nube.

La puerta de enlace de administración en la nube usa la siguiente característica de Microsoft Azure, que genera gastos en la cuenta de suscripción de Azure:

-   Máquina virtual

    -   En estos momentos, la puerta de enlace de administración en la nube necesita una máquina virtual Standard\_A2. Al crear el servicio, puede seleccionar cuántas máquinas virtuales va a admitir el servicio (una es el valor predeterminado).

    -   Solo con fines de estimación, tenga en cuenta que una única máquina virtual Standard\_A2 de Azure puede admitir aproximadamente 2000 clientes simultáneos basados en Internet.

    -   Vea la [Calculadora de precios de Azure](https://azure.microsoft.com/en-us/pricing/calculator/) para determinar los costos potenciales.

      >[!NOTE]
      >Los costos de máquina virtual varían según la región.

-   Transferencia de datos de salida

    -   Se incurren gastos por el flujo de datos fuera del servicio. Vea [Detalles de precios de ancho de banda de Azure](https://azure.microsoft.com/en-us/pricing/details/bandwidth/) para determinar los costos potenciales.

    -   Solo con fines de estimación, calcule aproximadamente 100 MB por cliente al mes para clientes basados en Internet que realizan actualizaciones de directivas cada hora.

    >[!NOTE]
    > Realizar otras acciones admitidas mediante la puerta de enlace de administración en la nube (por ejemplo, implementar actualizaciones de software o aplicaciones) aumentará la cantidad de transferencia de datos de salida de Azure.

-   Almacenamiento de contenido

    -   Los clientes basados en Internet que se administran con la puerta de enlace de administración en la nube obtendrán contenido de actualización de software desde Windows Update sin ningún costo.

    -   Cualquier otro contenido necesario (por ejemplo, aplicaciones) debe distribuirse a un punto de distribución basado en la nube. En estos momentos, Cloud Management Gateway solo admite el punto de distribución de nube para enviar contenido a los clientes.

    - Vea el costo de usar una [distribución basada en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes

[Configurar puerta de enlace de administración en la nube](setup-cloud-management-gateway.md)


## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Preguntas más frecuentes acerca de Cloud Management Gateway (CMG)

### <a name="why-use-the-cloud-management-gateway"></a>¿Por qué utilizar CMG?

Utilice este rol para simplificar la administración de clientes basada en Internet en tres pasos desde la consola de Configuration Manager.

1. Implemente CMG en Azure mediante el Asistente para [Cloud Management Gateway](/sccm/core/clients/manage/setup-cloud-management-gateway).
2. Configure el rol de sistema de sitio de [punto de conexión de CMG](/sccm/core/servers/deploy/configure/install-site-system-roles).
3. [Configure roles para el tráfico de CMG](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), como el punto de administración y el punto de actualización de software.

### <a name="how-does-the-cloud-management-gateway-work"></a>¿Cómo funciona CMG?

- El punto de conexión de CMG habilita una conexión coherente y de alto rendimiento desde Internet hasta la instancia de CMG.
- Configuration Manager publica la configuración de CMG, incluida la información de conexión y la configuración de seguridad.
- CMG autentica y reenvía las solicitudes de cliente de Configuration Manager al punto de conexión de CMG. Estas solicitudes se reenvían a los roles en la red corporativa según las asignaciones de direcciones URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>¿Cómo se implementa CMG?

El componente del administrador del servicio de nube en el punto de conexión del servicio administra todas las tareas de implementación de CMG. Además, supervisa y notifica la información de estado y el registro del servicio de Azure AD.

#### <a name="certificate-requirements"></a>Requisitos de certificados

Necesitará los siguientes certificados para proteger CMG:

- **Certificado de administración**: puede ser cualquier certificado, como los certificados autofirmados. Puede utilizar un certificado público cargado en Azure AD o un [PFX con clave privada](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importado en Configuration Manager para autenticarse con Azure AD. 
- **Certificado del servicio web**: recomendamos que utilice un certificado de entidad de certificación pública para obtener una confianza nativa por parte de los clientes. El registro CName debe crearse en el registrador de DNS público. No se admiten certificados comodín.
- **Carga de certificados de entidad de certificación raíz o subordinada a CMG**: CMG debe hacer la validación de cadena completa en los certificados PKI de cliente. Si usa una entidad de certificación de empresa para emitir certificados PKI de cliente y su entidad de certificación raíz o subordinada no está disponible en Internet, debe cargarla en CMG.

#### <a name="deployment-process"></a>Proceso de implementación

La implementación consta de dos pasos:

- Implementar el servicio de nube
    - Carga de su archivo de [esquema de definición de servicio de Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef)
    - Carga de su archivo de [esquema de configuración de servicio de Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg)
- Configurar el componente CMG en su servidor de Azure AD y establecer los parámetros de puntos de conexión, controladores HTTP y servicios de Internet Information Services (IIS)

Si cambia la configuración de CMG, se inicia una implementación de la configuración en CMG.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>¿Cómo garantiza CMG la seguridad?

CMG ayuda a garantizar la seguridad de las maneras siguientes:

- Acepta y administra las conexiones desde puntos de conexión de CMG, como la autenticación mutua de SSL que usa certificados internos e identificadores de conexión.
- Acepta y reenvía las solicitudes de cliente.
    - Autentica previamente las conexiones mediante el sistema mutuo de SSL en el certificado PKI del cliente.
    - La lista de confianza del certificado comprueba la raíz del certificado PKI del cliente. Puede especificar este parámetro en la configuración de comunicación del cliente en las propiedades del sitio. También realiza la misma validación que el punto de administración para el cliente.
    - Valida las direcciones URL recibidas.
    - Filtra las direcciones URL recibidas para comprobar si algún punto de conexión de CMG en conexión puede atender la solicitud de dirección URL.  
    - Comprueba la longitud de contenido para cada punto de conexión de la publicación.
    - Utiliza "round-robin" para equilibrar la carga entre los puntos de conexión de CMG desde el mismo sitio.

- Protege el punto de conexión de CMG.
    - Crea conexiones HTTP/ TCP coherentes a todas las instancias virtuales de la instancia de CMG en conexión. Comprueba y mantiene conexiones cada minuto.
    - Realiza la autenticación mutua de SSL con CMG mediante certificados internos.
    - Reenvía solicitudes HTTP basadas en asignaciones de direcciones URL.
    - Informa del estado de conexión para mostrar el estado de mantenimiento del servicio de administración.
    - Produce un informe de tráfico para cada punto de conexión cada 5 minutos.

- Protege al cliente de Configuration Manager del punto de conexión de publicación orientado a roles, como el punto de administración y los puntos de conexión del host del punto de actualización de software en ISS para atender las solicitudes del cliente. Cada punto de conexión publicado en CMG tiene una asignación de dirección URL.
La dirección URL externa es la que el cliente utiliza para comunicarse con CMG.
La dirección URL interna es el punto de conexión de CMG utilizado para reenviar las solicitudes al servidor interno. 

#### <a name="example"></a>Ejemplo:
Al habilitar el tráfico de CMG en un punto de administración, Configuration Manager crea un conjunto de asignaciones de direcciones URL internamente para cada servidor de punto de administración, como ccm_system, ccm_incoming y sms_mp.
La dirección URL externa para el punto de conexión ccm_system del punto de administración tendría este aspecto **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**. La dirección URL es única para cada punto de administración. El cliente de Configuration Manager pone entonces el nombre del punto de administración habilitado para CMG, como **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>**, en su lista del punto de administración de Internet. Todas las direcciones URL externas publicadas se cargan automáticamente en CMG para que este servicio pueda filtrarlas. Todas las asignaciones de direcciones URL se replican en el punto de conexión de CMG forma que las pueda reenviar a servidores internos en función del cliente que solicita la dirección URL externa.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>¿Qué puertos se usan por CMG? 

- No se necesitan puertos de entrada en la red local. La implementación de CMG creará varios de ellos en CMG automáticamente. 
- Además de 443, el punto de conexión de CMG necesita algunos puertos de salida.

|||||
|-|-|-|-|
|Flujo de datos|Server|Puertos de servidor|Cliente|
|Implementación de CMG|Azure|443|Punto de conexión de servicio de Configuration Manager|
|Canal de CMG de compilación|CMG|Instancia de VM: 1 Puerto: 443<br>Instancia de VM: N (N>=2 y N<= 16) Puertos: 10124~N 10140~N|Punto de conexión de CMG|
|Cliente a CMG|CMG|443|Cliente|
|Conector de CMG al rol de sitio (actualmente puntos de administración y puntos de actualización de software)|Rol de sitio|Protocolo y puertos configurados en el rol de sitio|Punto de conexión de CMG|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>¿Cómo se puede mejorar el rendimiento de CMG?

- Si es posible, configure CMG, el punto de conexión de CMG y el servidor de sitio de Configuration Manager en la misma región de red para reducir la latencia.
- Actualmente, la región no es relevante para la conexión entre el cliente de Configuration Manager y CMG.
- Para obtener alta disponibilidad, se recomiendan al menos 2 instancias virtuales de CMG y dos puntos de conexión de CMG por sitio. 
- Puede escalar CMG para que admita más clientes agregando más instancias de VM. El equilibrador de carga de Azure AD se ocupa de equilibrar su carga.
- Cree más puntos de conexión de CMG para distribuir la carga entre ellos. CMG aplicará el sistema "round-robin" en el tráfico de sus puntos de conexión de CMG en conexión.
- El número de cliente de soporte por instancia de VM de CMG es 6k en la versión 1702. Si el canal de CMG está sometido a una carga elevada, la solicitud se atenderá igualmente aunque quizá tarde algo más de lo normal.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>¿Cómo se puede supervisar el servicio Cloud Management Gateway?

Para solucionar problemas con implementaciones, use **CloudMgr.log** y **CMGSetup.log**.
Para solucionar problemas de estado del servicio, utilice **CMGService.log** y **SMS_CLOUD_PROXYCONNECTOR.log**.
Para solucionar problemas de tráfico de cliente, utilice **CMGHttpHandler.log**, **CMGService.Log** y **SMS_CLOUD_PROXYCONNECTOR.log**.

Para obtener una lista de todos los archivos de registro relacionados con CMG, consulte [Archivos de registro en System Center Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


