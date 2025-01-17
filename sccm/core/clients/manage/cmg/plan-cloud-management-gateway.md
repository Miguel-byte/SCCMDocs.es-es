---
title: Planear para Cloud Management Gateway
titleSuffix: Configuration Manager
description: Planee y diseñe Cloud Management Gateway (CMG) para simplificar la administración de clientes basados en Internet.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dff4d0ff8fe2bcb7fbbcd8b0b1c5c701f02d20fb
ms.sourcegitcommit: 159c6c9fe1df03fd2c4633125a593e3050a2f2da
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833175"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planificación de Cloud Management Gateway en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

<!--1101764-->
Cloud Management Gateway (CMG) proporciona una manera sencilla de administrar clientes de Configuration Manager en Internet. Al implementar CMG como un servicio en la nube de Microsoft Azure, puede administrar los clientes tradicionales que se mueven por Internet sin una infraestructura local adicional. Tampoco necesita exponer la infraestructura local a Internet.

> [!Note]  
> Configuration Manager no habilita esta característica opcional de forma predeterminada. Deberá habilitarla para poder usarla. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

Después de establecer los requisitos previos, la creación de CMG consta de los tres pasos siguientes en la consola de Configuration Manager:

1. Implementar el servicio en la nube de CMG en Azure.
2. Agregar el rol de punto de conexión de CMG.
3. Configurar el sitio y los roles de sitio para el servicio.
Una vez que lo haya implementado y configurado, los clientes podrán tener acceso sin problemas a los roles locales de sitio independientemente de si están en la intranet o en Internet.

En este artículo se proporcionan conceptos básicos para obtener información sobre CMG, diseñar cómo encaja en el entorno y planear la implementación.


## <a name="scenarios"></a>Escenarios

Hay varios escenarios en los que CMG resulta beneficioso. Los escenarios siguientes son algunos de los más comunes:  

- Administración de clientes tradicionales de Windows con la identidad unida a un dominio de Active Directory. Estos clientes incluyen Windows 7, Windows 8.1 y Windows 10. Usa certificados PKI para proteger el canal de comunicación. Entre las actividades de administración se incluyen las siguientes:  
    - Actualizaciones de software y Endpoint Protection
    - Estado de cliente y de inventario
    - Configuración de cumplimiento
    - Distribución de software para el dispositivo
    - Secuencia de tareas de actualización local de Windows 10

- Administración de clientes tradicionales de Windows 10 con identidad moderna, tanto híbridos como unidos a un dominio en la nube pura con Azure Active Directory (Azure AD). Los clientes usan Azure AD para la autenticación, en lugar de certificados PKI. Azure AD es más fácil de instalar, configurar y mantener que los sistemas PKI más complejos. Las actividades de administración son las mismas que el primer escenario, a las que se agregan la siguiente:  
    - Distribución de software para el usuario  

- Instalación del cliente de Configuration Manager en dispositivos Windows 10 a través de Internet. El uso de Azure AD permite que el dispositivo se autentique en CMG para el registro y la asignación de clientes. Puede instalar el cliente de forma manual o mediante otro método de distribución de software, como Microsoft Intune.  

- Aprovisionamiento de dispositivos nuevos con administración conjunta. Al inscribir automáticamente los clientes existentes, CMG no es necesario para la administración conjunta. Se necesita para nuevos dispositivos que implican Windows AutoPilot, Azure AD, Microsoft Intune y Configuration Manager. Para más información, consulte [Rutas hacia la administración conjunta](https://docs.microsoft.com/sccm/comanage/quickstart-paths).

### <a name="specific-use-cases"></a>Casos de uso específicos

En estos escenarios podrían aplicarse los siguientes casos de uso de dispositivos específicos:

- Dispositivos de itinerancia, como equipos portátiles.  

- Dispositivos remotos o de sucursales, que resultan menos costosos y más eficaces a la hora de administrarlos a través de Internet, en lugar de WAN o VPN.  

- Las fusiones y las adquisiciones, en las que puede ser más fácil unir dispositivos a Azure AD y administrarlos a través de CMG.  

> [!Important]
> De forma predeterminada, todos los clientes reciben una directiva para CMG y empiezan a usarla cuando están basados en Internet. Según cuál sea el escenario y el caso de uso que se aplique a la organización, es posible que tenga que definir el ámbito del uso de CMG. Para obtener más información, vea la configuración de cliente [Permitir que los clientes usen una instancia de Cloud Management Gateway](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).


## <a name="topology-design"></a>Diseño de topología

### <a name="cmg-components"></a>Componentes de CMG

La implementación y el funcionamiento de CMG incluye los componentes siguientes:  

- El **servicio en la nube de CMG** en Azure autentica y reenvía las solicitudes de cliente de Configuration Manager al punto de conexión de CMG.  

- El rol de sistema de sitio del **punto de conexión de CMG** permite una conexión coherente y de alto rendimiento desde la red local con el servicio de CMG en Azure. Además, publica la configuración de CMG, incluida la información de conexión y la configuración de seguridad. El punto de conexión de CMG reenvía las solicitudes de cliente desde CMG a los roles locales en función de las asignaciones de direcciones URL.

- El rol de sistema de sitio del [**punto de conexión del servicio**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) ejecuta el componente del administrador del servicio en la nube, que controla todas las tareas de implementación de CMG. Además, supervisa y notifica la información de estado y el registro del servicio de Azure AD. Asegúrese de que el punto de conexión del servicio está en [modo en línea](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- El rol de sistema de sitio del **punto de administración** atiende las solicitudes de cliente de manera normal.  

- El rol de sistema de sitio del **punto de actualización de software** atiende las solicitudes de cliente de manera normal.  

- Los **clientes basados en Internet** se conectan a CMG para tener acceso a los componentes locales de Configuration Manager.

- CMG usa un servicio web **HTTPS basado en certificados** para ayudar a proteger la comunicación de red con los clientes.  

- Los clientes basados en Internet usan **certificados PKI o Azure AD** para la identidad y la autenticación.  

- Un [**punto de distribución en la nube**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) proporciona contenido a los clientes basados en Internet según sea necesario.  

    - A partir de la versión 1806, una CMG también puede servir contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para obtener más información, vea [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificar una instancia de CMG).<!--1358651-->  

### <a name="azure-resource-manager"></a>Azure Resource Manager

<!-- 1324735 -->
Cree la instancia de CMG mediante una **implementación de Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) es una moderna plataforma para administrar todos los recursos de la solución como una única entidad, denominada [grupo de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Al implementar CMG con Azure Resource Manager, el sitio usa Azure Active Directory (Azure AD) para autenticar y crear los recursos necesarios en la nube. Esta implementación modernizada no requiere el certificado de administración de Azure clásico.  

> [!Note]  
> Esta función no habilita la compatibilidad de los proveedores de servicios en la nube (CSP) de Azure. La implementación de CMG con Azure Resource Manager sigue usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, consulte [Available Azure services in Azure CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services) (Servicios de Azure disponibles en los proveedores de servicios en la nube de Azure).

A partir de la versión 1902 de Configuration Manager, Azure Resource Manager es el único mecanismo de implementación para instancias nuevas de Cloud Management Gateway. Las implementaciones existentes seguirán funcionando.<!-- 3605704 -->

En la versión 1810 y versiones anteriores de Configuration Manager, el asistente de CMG seguirá proporcionando la opción de una **implementación del servicio clásico** mediante un certificado de administración de Azure. Para simplificar la implementación y la administración de recursos, se recomienda el modelo de implementación de Azure Resource Manager para todas las instancias nuevas de CMG. Si es posible, vuelva a implementar las instancias existentes de CMG a través de Resource Manager. Para obtener más información, vea [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificar una instancia de CMG).

> [!Important]  
> A partir de la versión 1810, la implementación del servicio clásico de Azure ya no se usa en Configuration Manager. Esta versión es la última que admite la creación de estas implementaciones de Azure. Esta funcionalidad se quitará en una edición futura de Configuration Manager.<!--SCCMDocs-pr issue #2993-->  

### <a name="hierarchy-design"></a>Diseño de jerarquía

Cree la instancia de CMG en el sitio de nivel superior de la jerarquía. Si es un sitio de administración central, cree puntos de conexión de CMG en sitios principales secundarios. El componente del administrador de servicios en la nube está en el punto de conexión de servicio, que también está en el sitio de administración central. Este diseño puede compartir el servicio en varios sitios principales si es necesario.

Puede crear varios servicios CMG en Azure y varios puntos de conexión de CMG. La existencia de varios puntos de conexión de CMG proporciona equilibrio de carga para el tráfico de cliente desde CMG a los roles locales. Para reducir la latencia de red, asigne la instancia de CMG asociada a la misma región geográfica que el sitio principal.

A partir de la versión 1902, puede asociar una instancia de CMG con un grupo de límites. Esta configuración permite a los clientes predeterminar o recurrir a dicha instancia de CMG para la comunicación con el cliente de acuerdo con las [relaciones de grupo de límites](/sccm/core/servers/deploy/configure/boundary-groups). Este comportamiento es especialmente útil en escenarios de sucursales y VPN. Puede dirigir el tráfico de clientes lejos de los enlaces WAN caros y lentos para utilizar servicios más rápidos en Microsoft Azure.<!--3640932-->

> [!Note]  
> Los clientes basados en Internet no pertenecen a ningún grupo de límites.
>
> En la versión 1810 y anteriores de Configuration Manager, la instancia de CMG no pertenece a ningún grupo de límites.

Otros factores, como el número de clientes que se van a administrar, también afectan al diseño de CMG. Para obtener más información, vea [Rendimiento y escalabilidad](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Ejemplo 1: sitio principal independiente

Contoso tiene un sitio principal independiente en un centro de datos local en su sede central de Nueva York.

- Crea una instancia de CMG en la región de Azure del Este de EE. UU. para reducir la latencia de red.
- Crea dos puntos de conexión de CMG, ambos vinculados al servicio CMG único.  

Cuando los clientes se mueven hacia Internet, se comunican con CMG en la región de Azure del Este de EE. UU. CMG reenvía esta comunicación a través de ambos puntos de conexión de CMG.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Ejemplo 2: jerarquía con una instancia de CMG específica del sitio

Fourth Coffee tiene un sitio de administración central en un centro de datos local en su sede de Seattle. Un sitio principal está en el mismo centro de datos y el otro sitio principal está en su oficina central europea, en París.

- En el sitio de administración central, crea dos servicios de CMG:
     - Una instancia de CMG en la región de Azure del Oeste de EE. UU.
     - Una instancia de CMG en la región de Azure de Europa Occidental.
- En el sitio principal basado en Seattle, crea un punto de conexión de CMG vinculado a la instancia de CMG del Oeste de EE. UU.
- En el sitio principal basado en París, crea un punto de conexión de CMG vinculado a la instancia de CMG de Europa Occidental.

Cuando los clientes de Seattle se mueven hacia Internet, se comunican con CMG en la región de Azure del Oeste de EE. UU. CMG reenvía esta comunicación al punto de conexión de CMG basado en Seattle.

Del mismo modo, cuando los clientes de París se mueven hacia Internet, se comunican con CMG en la región de Azure de Europa Occidental. CMG reenvía esta comunicación al punto de conexión de CMG basado en París. Cuando los usuarios de París viajan a la sede de la empresa en Seattle, sus equipos se siguen comunicando con la instancia de CMG de la región de Azure de Europa Occidental.

> [!Note]  
> Fourth Coffee consideró la posibilidad de crear otro punto de conexión de CMG en el sitio principal basado en París vinculado a la instancia de CMG del Oeste de EE. UU. Los clientes basados en París usarían ambas instancias de CMG, independientemente de su ubicación. Aunque esta configuración contribuye a equilibrar la carga del tráfico y proporciona redundancia de servicio, también puede provocar retrasos cuando los clientes de París se comunican con la instancia de CMG de Estados Unidos. Los clientes de Configuration Manager no conocen actualmente su región geográfica, por lo que no dan preferencia a una instancia de CMG que esté más cercana geográficamente, sino que usan de forma aleatoria una instancia de CMG que esté disponible.


## <a name="requirements"></a>requisitos

- Una **suscripción de Azure** para hospedar CMG.  

- Es necesario que un **administrador de Azure** participe en la creación inicial de determinados componentes, en función del diseño. Este rol no necesita permisos en Configuration Manager.  
    - Para implementar la instancia de CMG, necesita un **administrador de suscripciones**.
    - Para integrar el sitio con Azure AD a fin de implementar la instancia de CMG con Azure Resource Manager, necesita un **administrador global**.

- Al menos un servidor local de Windows para hospedar el **punto de conexión de CMG**. Puede colocalizar este rol con otros roles de sistema de sitio de Configuration Manager.  

- El **punto de conexión del servicio** debe estar en [modo en línea](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- Integración con **Azure AD** para implementar el servicio con Azure Resource Manager. Para obtener más información, vea [Configuración de servicios de Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Un [**certificado de autenticación de servidor**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth) para CMG.  

- Podrían ser necesarios **otros certificados**, según el modelo de autenticación y la versión del sistema operativo del cliente. Para obtener más información, vea [CMG certificates](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway) (Certificados de CMG).  

    A partir de la versión 1806, cuando se usa la opción del sitio **Usar los certificados generados por Configuration Manager para sistemas de sitios HTTP**, el punto de administración puede ser HTTP. Para obtener más información, vea [HTTP mejorado](/sccm/core/plan-design/hierarchy/enhanced-http).

- En la versión 1810 o anteriores de Configuration Manager, si se usa el método de implementación clásico de Azure, debe usar un [**certificado de automatización de Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_azuremgmt).  

    > [!TIP]  
    > Use el modelo de implementación de **Azure Resource Manager**. No necesita este certificado de administración.
    >
    > El método de implementación clásico está en desuso desde la versión 1810.  

- Los clientes deben usar **IPv4**.  


## <a name="specifications"></a>Especificaciones

- Todas las versiones de Windows que aparecen en [Sistemas operativos compatibles con dispositivos y clientes](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) son compatibles con CMG.  

- CMG solo admite los roles de punto de administración y punto de actualización de software.  

- CMG no es compatible con los clientes que solo se comunican con direcciones IPv6.<!--495606-->  

- Los puntos de actualización de software que usan un equilibrador de carga de red no funcionan con CMG. <!--505311-->  

- Las implementaciones de CMG que usan el modelo de implementación de Azure no permiten la compatibilidad con proveedores de servicios en la nube (CSP) de Azure. La implementación de CMG con Azure Resource Manager sigue usando el servicio en la nube clásico, que no es compatible con los proveedores de servicios en la nube. Para obtener más información, vea [Servicios de Azure disponibles en el programa CSP](https://docs.microsoft.com/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="support-for-configuration-manager-features"></a>Compatibilidad con características de Configuration Manager

En la tabla siguiente se muestra la compatibilidad de CMG con características de Configuration Manager:

|Característica  |Compatibilidad  |
|---------|---------|
| Actualizaciones de software     | ![Compatible.](media/green_check.png) |
| Endpoint Protection     | ![Compatible.](media/green_check.png) |
| Inventario de hardware y software     | ![Compatible.](media/green_check.png) |
| Estado de cliente y notificaciones     | ![Compatible.](media/green_check.png) |
| Ejecutar scripts     | ![Compatible.](media/green_check.png) |
| Configuración de cumplimiento     | ![Compatible.](media/green_check.png) |
| Instalación de cliente<br>(con integración de Azure AD)     | ![Compatible.](media/green_check.png) |
| Distribución de software (dirigida al dispositivo)     | ![Compatible.](media/green_check.png) |
| Distribución de software (dirigida al usuario, obligatorio)<br>(con integración de Azure AD)     | ![Compatible.](media/green_check.png) |
| Distribución de software (dirigida al usuario, disponible)<br>([todos los requisitos](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Compatible.](media/green_check.png) |
| Secuencia de tareas de actualización local de Windows 10      | ![Compatible.](media/green_check.png) |
| Secuencias de tareas que no usan imágenes de arranque y que se implementan con una opción: **Descargar todo el contenido localmente antes de iniciar la secuencia de tareas**      | ![Compatible.](media/green_check.png) |
| CMPivot     | ![Compatible.](media/green_check.png)  (1806) |
| Cualquier otro escenario de secuencia de tareas     | ![No compatible](media/Red_X.png) |
| Inserción de cliente     | ![No compatible](media/Red_X.png) |
| Asignación automática de sitio     | ![No compatible](media/Red_X.png) |
| Solicitudes de aprobación de software     | ![No compatible](media/Red_X.png) |
| Consola de Configuration Manager     | ![No compatible](media/Red_X.png) |
| Herramientas remotas     | ![No compatible](media/Red_X.png) |
| Sitio web de generación de informes     | ![No compatible](media/Red_X.png) |
| Wake on LAN     | ![No compatible](media/Red_X.png) |
| Clientes Mac, Linux y UNIX     | ![No compatible](media/Red_X.png) |
| Almacenamiento en caché del mismo nivel     | ![No compatible](media/Red_X.png) |
| MDM local     | ![No compatible](media/Red_X.png) |

|Clave|
|--|
|![Compatible.](media/green_check.png) = Esta característica es compatible con CMG en todas las versiones compatibles de Configuration Manager.  |
|![Compatible](media/green_check.png) (*AAMM*) = Esta característica es compatible con CMG a partir de la versión *AAMM* de Configuration Manager.  |
|![No compatible](media/Red_X.png) = Esta característica no se admite con CMG. |


## <a name="cost"></a>Coste

> [!IMPORTANT]  
> La siguiente información sobre los costos se indica solo con fines de estimación. Su entorno puede tener otras variables que afecten al costo general del uso de CMG.

CMG usa los siguientes componentes de Azure, que conllevan cargos en la cuenta de suscripción de Azure:

### <a name="virtual-machine"></a>Máquina virtual

- CMG usa Azure Cloud Services como plataforma como servicio (PaaS). Este servicio usa máquinas virtuales (VM) que conllevan costos de proceso.  

- CMG usa una máquina virtual estándar A2 V2.  

- Seleccione el número de instancias de máquina virtual que CMG admite. El valor predeterminado es una y el máximo es 16. Este número se establece al crear la instancia de CMG y se pueden cambiar posteriormente para escalar el servicio según sea necesario.

- Para obtener más información sobre cuántas máquinas virtuales necesita para sus clientes, vea [Rendimiento y escalabilidad](#performance-and-scale).

- Vea la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para determinar los costos potenciales.

    > [!NOTE]  
    > Los costos de máquina virtual varían según la región.

### <a name="outbound-data-transfer"></a>Transferencia de datos de salida

- Los cargos se basan en los datos que fluyen fuera de Azure (salida o descarga). Todos los datos que fluyan a Azure son gratuitos (entrada o carga). Los flujos de datos de CMG fuera de Azure incluyen la directiva para el cliente, las notificaciones de cliente y las respuestas del cliente reenviadas por la CMG al sitio. Estas respuestas incluyen informes de inventario, mensajes de estado y estado de cumplimiento.  

- Incluso aunque ningún cliente se comunique con CMG, algún tipo de comunicación de fondo genera tráfico de red entre CMG y el sitio local.  

- Vea la **transferencia de datos de salida (GB)** en la consola de Configuration Manager. Para obtener más información, vea [Monitor clients on CMG](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway) (Supervisar clientes en CMG).  

- Vea [Detalles de precios de ancho de banda de Azure](https://azure.microsoft.com/pricing/details/bandwidth/) para determinar los costos potenciales. Los precios de la transferencia de datos se organizan por plan de tarifa. Cuanto más uso haga, menos pagará por gigabyte.  

- *Solo con fines de estimación*, calcule aproximadamente 100-300 MB por cliente al mes para clientes basados en Internet. La estimación más baja es la de una configuración de cliente predeterminada. La estimación más alta es la de una configuración de cliente más agresiva. El uso real puede variar en función de la configuración del cliente.  

    > [!NOTE]  
    > Si realiza otras acciones, como implementar actualizaciones de software o aplicaciones, aumentará la cantidad de transferencia de datos de salida de Azure.

- La configuración errónea de la opción CMG para **comprobar la revocación de certificado de cliente**  puede generar tráfico adicional desde los clientes a CMG. Este tráfico adicional puede aumentar los datos de salida de Azure, lo que podría aumentar los costos de Azure.<!-- SCCMDocs#1434 --> Para obtener más información, vea [Publicar la lista de revocación de certificados](https://docs.microsoft.com/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway#bkmk_crl).  

### <a name="content-storage"></a>Almacenamiento de contenido

- Los clientes basados en Internet obtienen contenido de actualización de software de Microsoft desde Windows Update sin ningún costo. No distribuya paquetes de actualización con contenido de actualización de Microsoft a un punto de distribución en la nube, ya que podría conllevar costos de almacenamiento y salida de datos.  

- Para otros contenidos necesarios, como aplicaciones o actualizaciones de software de terceros, debe distribuir a un punto de distribución en la nube. En estos momentos, CMG solo admite el punto de distribución en la nube para enviar contenido a los clientes.  

- Para obtener más información, vea el costo de la utilización de [puntos de distribución en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

- A partir de la versión 1806, una instancia de CMG también puede ser un punto de distribución en la nube para brindar contenido a los clientes. Esta funcionalidad reduce los certificados necesarios y el costo de máquinas virtuales de Azure. Para obtener más información, vea [Modify a CMG](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg) (Modificar una instancia de CMG).<!--1358651-->  

### <a name="other-costs"></a>Otros costos

- Todos los servicios en la nube tienen una dirección IP dinámica. Cada instancia de CMG diferente usa una nueva dirección IP dinámica. El hecho de agregar máquinas virtuales adicionales por CMG no aumenta estas direcciones.  


## <a name="performance-and-scale"></a>Rendimiento y escalabilidad

Para obtener más información sobre la escala CMG, vea [Números de tamaño y escala](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

Las siguientes recomendaciones le ayudarán a mejorar el rendimiento de CMG:

- Si es posible, configure CMG, el punto de conexión de CMG y el servidor de sitio de Configuration Manager en la misma región de red para reducir la latencia.  

- La región no es relevante para la conexión entre el cliente de Configuration Manager y CMG. La comunicación del cliente no se ve afectada en gran medida por la latencia o la separación geográfica. No es necesario implementar varias instancias de CMG para la finalidad de proximidad geográfica. Implemente la instancia de CMG en el sitio de nivel superior de la jerarquía y agregue instancias para aumentar la escala.

- Para una alta disponibilidad del servicio, cree una instancia de CMG con al menos dos servicios y dos puntos de conexión de CMG por sitio.  

- Escale CMG para que admita más clientes mediante la adición de más instancias de máquina virtual. El equilibrador de carga de Azure controla las conexiones de cliente con el servicio.  

- Cree más puntos de conexión de CMG para distribuir la carga entre ellos. CMG aplica el sistema round robin para distribuir el tráfico a sus puntos de conexión de CMG en conexión.  

- Cuando CMG soporta una carga elevada con más del número de clientes es mayor que el admitido, sigue administrando las solicitudes, pero pueden producirse retrasos.  

> [!Note]  
> Mientras que Configuration Manager no tiene un límite máximo para el número de clientes de un punto de conexión de CMG, Windows Server tiene un intervalo máximo de puertos dinámicos TCP predeterminado de 16 384. Si un sitio de Configuration Manager administra más de 16 384 clientes con un solo punto de conexión de CMG, debe aumentar el límite de Windows Server. Todos los clientes mantienen un canal para las notificaciones de cliente, que contiene un puerto abierto en el punto de conexión de CMG. Para obtener más información sobre cómo usar el comando netsh para aumentar este límite, vea el [artículo 929851 del Soporte técnico de Microsoft ](https://support.microsoft.com/help/929851).


## <a name="ports-and-data-flow"></a>Puertos y flujo de datos

No es necesario abrir ningún puerto de entrada a la red local. El punto de conexión de servicio y el punto de conexión de CMG inician todas las comunicaciones con Azure y CMG. Estos dos roles de sistema de sitio deben poder crear conexiones de salida a la nube de Microsoft. El punto de conexión de servicio implementa y supervisa el servicio de Azure, por lo que debe estar en modo en línea. El punto de conexión de CMG conecta con CMG para administrar las comunicaciones entre los roles de sistema de sitio de CMG y local.

El diagrama siguiente es un flujo de datos conceptual básico para CMG:

![Flujo de datos de CMG](media/cmg-data-flow.png)

1. El punto de conexión de servicio conecta con Azure a través del puerto HTTPS 443. Para la autenticación, usa Azure AD o el certificado de administración de Azure. El punto de conexión de servicio implementa CMG en Azure. CMG crea el servicio en la nube HTTPS con mediante certificado de autenticación de servidor.  

2. El punto de conexión de CMG se conecta a CMG en Azure a través de TCP-TLS o HTTPS. Mantiene la conexión abierta y crea el canal para la comunicación bidireccional futura.  

3. El cliente se conecta a CMG a través del puerto HTTPS 443. Para la autenticación, usa Azure AD o el certificado de autenticación de cliente.  

4. CMG reenvía la comunicación de cliente a través de la conexión existente al punto de conexión de CMG local. No es necesario abrir ningún puerto de firewall de entrada.  

5. El punto de conexión de CMG reenvía la comunicación de cliente al punto de administración local y al punto de actualización de software.  

Para más información sobre hospedar contenido en Azure, consulte [Usar un punto de distribución basado en la nube](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).

### <a name="required-ports"></a>Puertos necesarios

En esta tabla se enumeran los protocolos y los puertos de red requeridos. El *cliente* es el dispositivo que inicia la conexión y requiere un puerto de salida. El *servidor* es el dispositivo que acepta la conexión y requiere un puerto de entrada.

| Cliente  | Protocolo | Puerto  | Server  | Descripción  |
|---------|---------|---------|---------|---------|
| Punto de conexión de servicio     | HTTPS | 443        | Azure        | Implementación de CMG |
| Punto de conexión de CMG     |  TCP-TLS | 10140-10155        | Servicio de CMG        | Protocolo preferido para crear el canal de CMG <sup>1</sup> |
| Punto de conexión de CMG     | HTTPS | 443        | Servicio de CMG       | Protocolo de reserva para crear el canal de CMG para una sola instancia de máquina virtual<sup>2</sup> |
| Punto de conexión de CMG     |  HTTPS   | 10124-10139     | Servicio de CMG       | Protocolo de reserva para crear el canal de CMG para dos o más instancias de máquina virtual<sup>3</sup> |
| Cliente     |  HTTPS | 443         | CMG        | Comunicación de cliente general |
| Punto de conexión de CMG      | HTTPS o HTTP | 443 o 80         | Punto de administración<br>(versión 1710) | Para el tráfico local, el puerto depende de la configuración del punto de administración |
| Punto de conexión de CMG      | HTTPS | 443      | Punto de administración<br>(versión 1802) | El tráfico local debe ser HTTPS |
| Punto de conexión de CMG      | HTTPS o HTTP | 443 o 80         | Punto de actualización de software | Para el tráfico local, el puerto depende de la configuración del punto de actualización de software |

<sup>1</sup> El punto de conexión de CMG primero intenta establecer una conexión TCP-TLS de larga duración con cada instancia de máquina virtual de CMG. Se conecta a la primera instancia de máquina virtual en el puerto 10140. La segunda instancia de máquina virtual usa el puerto 10141, hasta la decimosexta en el puerto 10155. Una conexión TCP-TLS tiene un mejor rendimiento, pero no es compatible con un proxy de Internet. Si el punto de conexión de CMG no se puede conectar a través de TCP-TLS, recurre a HTTPS<sup>2</sup>.  

<sup>2</sup> Si el punto de conexión de CMG no se puede conectar a CMG a través de TCP-TLS<sup>1</sup>, se conecta al equilibrador de carga de red de Azure a través de HTTPS 443 solo para una instancia de máquina virtual.  

<sup>3</sup> Si hay dos o más instancias de máquina virtual, el punto de conexión de CMG usa HTTPS 10124 para la primera instancia de máquina virtual, no HTTPS 443. Se conecta a la segunda instancia de máquina virtual en HTTPS 10125, hasta la decimosexta en el puerto HTTPS 10139.

### <a name="internet-access-requirements"></a>Requisitos de acceso a Internet

Si la organización restringe la comunicación de red con Internet a través de un dispositivo proxy o firewall, necesita permitir que el punto de conexión de CMG y el punto de conexión de servicio accedan a los puntos de conexión de Internet.

Para más información, consulte los [requisitos de acceso a Internet](/sccm/core/plan-design/network/internet-endpoints#bkmk_cloud).


## <a name="next-steps"></a>Pasos siguientes

- [Certificados para la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Seguridad y privacidad de la puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Números de tamaño y escala de System Center Configuration Manager](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Preguntas más frecuentes sobre Cloud Management Gateway](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurar puerta de enlace de administración en la nube](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
