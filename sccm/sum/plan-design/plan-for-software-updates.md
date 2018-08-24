---
title: Planear las actualizaciones de software
titleSuffix: Configuration Manager
description: Es imprescindible planear la infraestructura de punto de actualización de software antes de usar las actualizaciones de software en un entorno de producción de Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 807204b9a64e36e103a32d553e7804a0a8592ec1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383812"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planear actualizaciones de software en Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Antes de usar las actualizaciones de software en un entorno de producción de Configuration Manager, es importante que siga el proceso de planeamiento. Tener un buen plan para la infraestructura de punto de actualización de software es la clave para conseguir una correcta implementación de actualizaciones de software.



## <a name="capacity-planning-recommendations-for-software-updates"></a>Recomendaciones para la planeación de capacidad para las actualizaciones de software  

Esta sección incluye los subtemas siguientes:  
- [Planeación de la capacidad para el punto de actualización de software](#BKMK_SUMCapacity)
- [Planeación de la capacidad para los objetos de actualizaciones de software](#bkmk_sum-capacity-obj)  


Utilice las siguientes recomendaciones como una línea de base. Esta línea de base le ayuda a determinar la información para la planeación de la capacidad de las actualizaciones de software que sea adecuada para su organización. Los requisitos reales de capacidad pueden variar respecto a los incluidos en las recomendaciones de este artículo, en función de los siguientes criterios: 
- El entorno de red específico
- El hardware que se usa para hospedar el punto de actualización de software del sistema de sitio
- El número de clientes administrados
- Los otros roles de sistema de sitio instalados en el servidor  


###  <a name="BKMK_SUMCapacity"></a> Planeación de la capacidad para el punto de actualización de software  

El número de clientes admitidos depende de la versión de Windows Server Update Services (WSUS) que se ejecuta en el punto de actualización de software. También depende de si el rol de sistema de sitio del punto de actualización de software coexiste con otro rol de sistema de sitio:  

-   El punto de actualización de software puede admitir hasta 25 000 clientes cuando WSUS se ejecuta en el servidor del punto de actualización de software y este punto coexiste con otro rol de sistema de sitio.  

-   El punto de actualización de software puede admitir hasta 150 000 clientes cuando un servidor remoto cumple los requisitos de WSUS, WSUS se utiliza con Configuration Manager y configura las siguientes opciones:

    Grupos de aplicaciones de IIS:
    - Aumente la longitud de cola de WsusPool a 2000
    - Cuadriplique el límite de memoria privada de WsusPool o defínalo en 0 (ilimitado). Por ejemplo, si el límite predeterminado es 1 843 200 KB, auméntelo a 7 372 800. Para más información, vea esta [entrada del blog del equipo de soporte técnico de Configuration Manager](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Para más información sobre los requisitos de hardware para el punto de actualización de software, vea [Requisitos recomendados para sistemas de sitio](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).  


### <a name="bkmk_sum-capacity-obj"></a> Planeación de la capacidad para los objetos de actualizaciones de software  

Utilice la siguiente información de capacidad para planear los objetos de actualizaciones de software:  

#### <a name="limit-of-1000-software-updates-in-a-deployment"></a>Límite de 1.000 actualizaciones de software en una implementación  
Limite el número de actualizaciones de software a 1000 por cada implementación de actualización de software. Cuando crea una regla de implementación automática (ADR), especifique un criterio que limite el número de actualizaciones de software. La regla de implementación automática produce un error cuando los criterios especificados devuelven más de 1000 actualizaciones de software. Compruebe el estado de la ADR desde el nodo **Reglas de implementación automática** de la consola de Configuration Manager. Al implementar manualmente las actualizaciones de software, no seleccione más de 1000 actualizaciones para implementar.  

Limite también el número de actualizaciones de software a 1000 en una línea base de configuración. Para obtener más información, consulte [Crear una línea base de configuración](/sccm/compliance/deploy-use/create-configuration-baselines).



##  <a name="BKMK_SUPInfrastructure"></a> Determinar la infraestructura del punto de actualización de software  

Esta sección incluye los subtemas siguientes:    
- [Lista de puntos de actualización de software](#BKMK_SUPList)
- [Cambio de punto de actualización de software](#BKMK_SUPSwitching)
- [Cambio manual de clientes a un nuevo punto de actualización de software](#BKMK_ManuallySwitchSUPs)
- [Puntos de actualización de software en un bosque que no es de confianza](#BKMK_SUP_CrossForest)
- [Usar servidor WSUS existente como origen de la sincronización en el sitio de nivel superior](#BKMK_WSUSSyncSource)
- [Punto de actualización de software en un sitio secundario](#BKMK_SUPSecSite)  
- [Planear los clientes basados en Internet](#bkmk_internet-clients)  
- [Planear el contenido de actualización de software](#bkmk_content)  
- [Planear las actualizaciones de terceros](#bkmk_thirdparty)  


El sitio de administración central y todos los sitios primarios secundarios deben tener un punto de actualización de software. Cuando planee la infraestructura del punto de actualización de software, determine las siguientes dependencias:
 - Dónde instalar el punto de actualización de software para el sitio  
 - Qué sitios requieren un punto de actualización de software que acepte comunicaciones procedentes de clientes basados en Internet
 - Si necesita un punto de actualización de software en un sitio secundario  

> [!IMPORTANT]  
>  Para obtener más información sobre las dependencias internas y externas que se requieren para las actualizaciones de software, consulte [Requisitos previos para las actualizaciones de software](prerequisites-for-software-updates.md).  

Agregue varios puntos de actualización de software en un sitio primario de Configuration Manager para proporcionar tolerancia a errores. El diseño de conmutación por error del punto de actualización de software difiere del modelo de selección aleatoria pura que se utiliza en el diseño de los puntos de administración. A diferencia del diseño de los puntos de administración, hay costes de rendimiento de red y de cliente en el diseño del punto de actualización de software cuando los clientes cambian a un nuevo punto de actualización de software. Cuando el cliente cambia a un servidor de WSUS nuevo para explorar actualizaciones de software, el resultado es un aumento del tamaño del catálogo, y demandas de rendimiento de red y de cliente asociadas. Por tanto, el cliente conserva la afinidad con el último punto de actualización de software que exploró satisfactoriamente.  

El primer punto de actualización de software que se instala en un sitio primario es el origen de sincronización para todos los puntos de actualización de software adicionales que se agregan al sitio primario. Después de haber agregado los puntos de actualización de software y de haber iniciado la sincronización, vea el estado de dichos puntos y el origen de sincronización en el nodo **Estado de sincronización de punto de actualización de software** del área de trabajo **Supervisión**.  

Cuando se produzca un error de punto de actualización de software configurado como origen de sincronización para el sitio, quite manualmente el rol con errores. Después, seleccione un nuevo punto de actualización de software que se usará como el origen de sincronización. Para obtener más información, vea [Quitar el rol de sistema de sitio de punto de actualización de software](../get-started/remove-a-software-update-point.md).  


###  <a name="BKMK_SUPList"></a> Lista de puntos de actualización de software  

Configuration Manager proporciona al cliente una lista de puntos de actualización de software en los siguientes escenarios:  

- Un nuevo cliente recibe la directiva para habilitar las actualizaciones de software  

- Un cliente no puede ponerse en contacto con su punto de actualización de software asignado y necesita cambiar a otro  

El cliente selecciona aleatoriamente un punto de actualización de software en la lista. Da prioridad a los puntos de actualización de software en el mismo bosque. Configuration Manager proporciona clientes de otra lista según el tipo de cliente:  

-   **Clientes basados en intranet**: recibe una lista de puntos de actualización de software que puede configurar para permitir conexiones solo desde la intranet, o una lista de puntos de actualización de software que permiten las conexiones de cliente de Internet o intranet.  

-   **Clientes basados en Internet**: reciben una lista de puntos de actualización de software que se configuran para permitir conexiones provenientes de Internet solamente o una lista de puntos de actualización de software que permiten conexiones de cliente a Internet e intranet.  


###  <a name="BKMK_SUPSwitching"></a> Cambio de punto de actualización de software  

> [!NOTE]  
> Los clientes usan grupos de límites para buscar un punto de actualización de software nuevo. Si su punto de actualización de software actual ya no es accesible, también usan grupos de límites para reservar y buscar uno nuevo. Agregue puntos de actualización de software individuales a otros grupos de límites para controlar qué servidores puede buscar un cliente. Para obtener más información, vea [Puntos de actualización de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  

Si tiene varios puntos de actualización de software en un sitio y uno deja de estar disponible o genera errores, los clientes se conectarán a otro punto de actualización de software. Con este nuevo servidor, los clientes continuarán con la exploración para detectar las actualizaciones de software más recientes. Cuando a un cliente se le asigna por primera vez un punto de actualización de software, permanece asignado a ese punto de actualización de software a no ser que no pueda explorar.  

La exploración para la detección de actualizaciones de software puede producir un error con un número diferente de códigos de error de reintentos y de no reintentos. Cuando la exploración produce un código de error de reintento, el cliente inicia un proceso de reintento para explorar las actualizaciones de software en el punto de actualización de software. Las condiciones de alto nivel que dan como resultado un código de error de reintento suelen producirse porque el servidor de WSUS no está disponible o porque está temporalmente sobrecargado. Cuando se produce un error al explorar para detectar actualizaciones de software, el cliente utiliza el siguiente proceso:  

1.  El cliente explora para detectar actualizaciones de software:  
    - A su hora programada
    - Cuando se ejecuta manualmente desde el panel de control en el cliente
    - Cuando se ejecuta manualmente desde la consola de Configuration Manager a través de una acción de notificación de cliente
    - Cuando se ejecuta desde un método de SDK de Configuration Manager  

2.  Si se produce un error en el examen, el cliente espera 30 minutos para reintentarlo. Usa el mismo punto de actualización de software.  

3.  El cliente lo reintenta un mínimo de cuatro veces cada 30 minutos. Después del cuarto error, y tras esperar otros dos minutos, el cliente pasa al siguiente punto de actualización de software de su lista.  

4.  El cliente repite este proceso con el nuevo punto de actualización de software. Después de un examen correcto, el cliente se conecta con el nuevo punto de actualización de software.  

En la lista siguiente se ofrece información adicional que puede tener en cuenta en los escenarios de cambio y reintento de puntos de actualización de software:  

-   Si un cliente se desconecta de la intranet y no puede explorar para detectar actualizaciones de software, no se cambia a otro punto de actualización de software. Este es un error esperado, dado que el cliente no puede conectarse a la red interna ni a un punto de actualización de software que permite conexiones desde la intranet. El cliente de Configuration Manager determina la disponibilidad del punto de actualización de software de la intranet.  

-   Si está administrando clientes en Internet y ha configurado varios puntos de actualización de software para aceptar la comunicación de clientes en Internet, el proceso de cambio sigue el proceso de reintento estándar descrito anteriormente.  

-   Si se inició el proceso de exploración, pero el cliente se desconectó antes de completarse la exploración, no se considera un error y no cuenta como uno de los cuatro reintentos.  

Si Configuration Manager recibe alguno de los siguientes códigos de error del Agente de Windows Update, el cliente vuelve a intentar la conexión:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Para buscar el significado de un código de error, convierta el código de error decimal en hexadecimal y después busque el valor hexadecimal en un sitio como la wiki [Windows Update Agent - Error Codes](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Códigos de error del Agente de Windows Update). Por ejemplo, el código de error decimal 2149842970 es 8024001A en hexadecimal, lo que significa WU_E_POLICY_NOT_SET No se estableció un valor de directiva.  


###  <a name="BKMK_ManuallySwitchSUPs"></a> Cambio manual de clientes a un nuevo punto de actualización de software

Cambie los clientes de Configuration Manager a un nuevo punto de actualización de software cuando haya problemas con el punto de actualización de software activo. Este cambio solo sucede cuando un cliente recibe varios puntos de actualización de software desde un punto de administración.

> [!IMPORTANT]    
> Cuando cambia de dispositivo para usar un nuevo servidor, los dispositivos utilizan la reserva para buscar ese servidor nuevo. Antes de iniciar este cambio, revise las configuraciones de los grupos de límites para asegurarse de que los puntos de actualización de software se encuentran en los grupos de límites correctos. Para obtener más información, vea [Puntos de actualización de software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  
>
> El cambio a un nuevo punto de actualización de software genera tráfico de red adicional. La cantidad de tráfico depende de las opciones de configuración de WSUS, por ejemplo, los productos y clasificaciones sincronizados o el uso de una base de datos WSUS compartida. Si planea cambiar varios dispositivos, considere la posibilidad de hacerlo durante las ventanas de mantenimiento. Este tiempo reduce el impacto en la red cuando los clientes examinan con el nuevo punto de actualización de software.  

#### <a name="process-to-switch-software-update-points"></a>Proceso para cambiar puntos de actualización de software  
Inicie este cambio en una colección de dispositivos. Una vez iniciado, los clientes buscarán otro punto de actualización de software en el siguiente examen.  

1.  En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad** y seleccione el nodo **Recopilaciones de dispositivos**.  

2.  Seleccione la colección de destino. En la pestaña de la cinta **Inicio** del grupo **Colección**, haga clic en **Notificación de cliente** y luego en **Cambiar al siguiente punto de actualización de software**.  


###  <a name="BKMK_SUP_CrossForest"></a> Puntos de actualización de software en un bosque que no es de confianza  

Cree uno o varios puntos de actualización de software en un sitio para admitir a clientes de un bosque que no es de confianza. Para agregar un punto de actualización de software en otro bosque, debe instalar y configurar un servidor de WSUS en el bosque. Después, inicie el asistente para agregar un servidor de sitio de Configuration Manager con el rol de sistema de sitio del punto de actualización de software. En el asistente, configure las siguientes opciones para conectarse correctamente a WSUS en el bosque que no es de confianza:  

-   Especifique una **cuenta de instalación del sistema de sitio** que pueda acceder al servidor WSUS en el bosque que no es de confianza.  

-   Especifique una **cuenta de conexión del servidor WSUS** que se va a utilizar para conectarse al servidor WSUS.  

Por ejemplo, tiene un sitio primario en el bosque A con dos puntos de actualización de software (SUP01 y SUP02). Para el mismo sitio primario también tiene dos puntos de actualización de software (SUP03 y SUP04) en el bosque B. Al cambiar al siguiente punto de actualización de software, el cliente da prioridad a los servidores del mismo bosque.  


###  <a name="BKMK_WSUSSyncSource"></a> Usar servidor WSUS existente como origen de la sincronización en el sitio de nivel superior  

Normalmente, el sitio de nivel superior de la jerarquía está configurado para sincronizar los metadatos de las actualizaciones de software con Microsoft Update. Si su directiva de seguridad de la organización no permite al sitio de nivel superior acceder a Internet, puede configurar el origen de la sincronización del sitio de nivel superior para utilizar un servidor WSUS existente. Este servidor WSUS no está en su jerarquía de Configuration Manager. Por ejemplo, tiene un servidor WSUS en una red conectada a Internet (red perimetral), pero el sitio de nivel superior se encuentra en una red interna sin acceso a Internet. Configure el servidor WSUS de la red perimetral como origen de la sincronización para los metadatos de las actualizaciones de software. Configure el servidor WSUS en la red perimetral para sincronizar las actualizaciones de software con los mismos criterios que necesite en Configuration Manager. De lo contrario, es posible que el sitio de nivel superior no sincronice las actualizaciones de software previstas. Cuando instale el punto de actualización de software, configure una cuenta de conexión de servidor WSUS. Esta cuenta necesita acceso al servidor WSUS en la red perimetral. Confirme también que el firewall permite el tráfico en los puertos correspondientes. Para obtener más información, vea los [puertos que usa el punto de actualización de software para el origen de la sincronización](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS).  


###  <a name="BKMK_SUPSecSite"></a> Punto de actualización de software en un sitio secundario  

El punto de actualización de software es opcional en un sitio secundario. Instale solo un punto de actualización de software en un sitio secundario. Cuando un punto de actualización de software no se instala en el sitio secundario, los dispositivos en los límites de un sitio secundario usan un punto de actualización de software en su sitio primario asignado. Se suele instalar un punto de actualización de software en un sitio secundario cuando el ancho de banda de red es limitado entre los dispositivos del sitio secundario y los puntos de actualización de software del sitio primario principal. También puede usar esta configuración cuando el punto de actualización de software en el sitio primario se aproxime al límite de capacidad. Una vez haya instalado y configurado correctamente un punto de actualización de software en el sitio secundario, se actualiza una directiva para todo el sitio para los clientes, que empezarán a utilizar el nuevo punto de actualización de software.  


### <a name="bkmk_internet-clients"></a> Planear los clientes basados en Internet

Cuando necesite administrar dispositivos que salen de la red y pasan a usar Internet, deberá desarrollar un plan para la administración de las actualizaciones de software en estos dispositivos. Configuration Manager admite varias tecnologías para este escenario. Use una o una combinación de varias según sea necesario para cumplir los requisitos de su organización.

#### <a name="cloud-management-gateway"></a>Puerta de enlace de administración en la nube
Cree una puerta de enlace de administración en la nube en Microsoft Azure y habilite al menos un punto de actualización de software en el entorno local para permitir el tráfico desde clientes basados en Internet. Cuando los clientes pasen a usar Internet, seguirán buscando sus puntos de actualización de software. Todos los clientes basados en Internet obtienen siempre el contenido desde el servicio en la nube de Microsoft Update. 

Para obtener más información, vea [Planificación de Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="internet-based-client-management"></a>Administración de cliente basada en Internet
Coloque un punto de actualización de software en una red con conexión a Internet y habilítelo para permitir el tráfico desde clientes basados en Internet. A medida que los clientes se conecten a Internet, cambiarán a este punto de actualización de software para el análisis. Todos los clientes basados en Internet obtienen siempre el contenido desde el servicio en la nube de Microsoft Update.

Para obtener más información sobre las ventajas y desventajas de la administración de clientes basados en Internet, vea [Administrar clientes en Internet](/sccm/core/clients/manage/manage-clients-internet).

#### <a name="windows-update-for-business"></a>Windows Update para empresas
Windows Update for Business permite mantener los dispositivos Windows 10 siempre al día con las actualizaciones de características y calidad más recientes. Estos dispositivos se conectan directamente al servicio en la nube de Windows Update. Configuration Manager puede diferenciar entre los equipos con Windows 10 que usan WUfB y WSUS para obtener actualizaciones de software.

Para obtener más información, consulte [Integración con Windows Update for Business](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).


### <a name="bkmk_content"></a> Planear el contenido de actualización de software

Los clientes deben descargar los archivos de contenido para las actualizaciones de software para poder instalarlas. Configuration Manager proporciona varias tecnologías para admitir la administración y entrega de este contenido. También puede configurar las implementaciones de actualizaciones de software para permitir o requerir a los clientes que obtengan el contenido directamente desde el servicio en la nube de Microsoft Update.

#### <a name="download-and-distribute-content"></a>Descargar y distribuir contenido 
De forma predeterminada, el proceso de administración de actualizaciones de software en Configuration Manager usa las características de administración de contenido integradas. Estas características incluyen la biblioteca de contenido del almacén de instancia única centralizada y el diseño distribuido de la función de sistema de sitio del punto de distribución. Utilice estas características al descargar y distribuir paquetes de implementación de actualizaciones de software. 

Para obtener más información, vea [Descargar actualizaciones de software](/sccm/sum/deploy-use/download-software-updates).

#### <a name="manage-express-installation-files-for-windows-10"></a>Administración de archivos de instalación rápida para Windows 10
Configuration Manager admite el uso de archivos de instalación rápida para las actualizaciones de Windows 10. Los archivos de actualización rápida y las tecnologías de apoyo como la optimización de entrega pueden ayudar a reducir el impacto en la red de archivos de contenido grandes que se descargan a los clientes. 

Para obtener más información, vea [Optimización de la distribución de actualizaciones de Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

#### <a name="clients-download-content-from-the-internet"></a>Los clientes descargan contenido desde Internet
Al implementar las actualizaciones de software en los clientes, configure la implementación para que los clientes descarguen contenido desde el servicio en la nube de Microsoft Update. Si los clientes no pueden descargar contenido desde otro origen de contenido, pueden seguir descargando el contenido desde Internet. 

A partir de la versión 1806, no tiene que crear un paquete de implementación al implementar las actualizaciones de software. Cuando seleccione la opción **Ningún paquete de implementación**, los clientes pueden seguir descargando contenido desde orígenes locales, si está disponible, pero normalmente descargarán desde el servicio Microsoft Update.<!--1357933-->

Los clientes basados en Internet descargan siempre el contenido desde el servicio en la nube de Microsoft Update. No distribuya paquetes de implementación de actualizaciones de software a un punto de distribución en la nube. Se le cobra por almacenamiento en el punto de distribución en la nube, pero los clientes no van a descargar estos paquetes. 


### <a name="bkmk_thirdparty"></a> Planear las actualizaciones de terceros
Configuration Manager se integra con WSUS, que admite de forma nativa las actualizaciones de software publicadas por Microsoft. La mayoría de los clientes utiliza otras aplicaciones de terceros que también necesitan actualizaciones. Hay varias opciones que se deben tener en cuenta para mantener actualizadas las aplicaciones de terceros.

#### <a name="supersede-applications-to-update"></a>Sustituir aplicaciones para actualizar
Use una relación de sustitución con la administración de aplicaciones de Configuration Manager para actualizar o sustituir aplicaciones existentes. Cuando se sustituye una aplicación, se puede especificar un tipo de implementación nuevo para reemplazar el de la aplicación sustituida. También puede decidir si quiere actualizar o desinstalar la aplicación sustituida antes de que se instale la aplicación que sustituye.

Para obtener más información, vea [Revisar y sustituir aplicaciones](/sccm/apps/deploy-use/revise-and-supersede-applications).

#### <a name="third-party-software-updates"></a>Actualizaciones de software de terceros
A partir de la versión 1806, puede usar el nodo **Catálogos de actualizaciones de software de terceros** de la consola de Configuration Manager para suscribirse a catálogos de terceros, publicar sus actualizaciones en el punto de actualización de software e implementarlas posteriormente en los clientes.<!--1352101-->

Para obtener más información, vea [Third-party software updates (Actualizaciones de software de terceros)](/sccm/sum/deploy-use/third-party-software-updates).

#### <a name="system-center-updates-publisher"></a>Editor de actualizaciones de System Center
System Center Updates Publisher (SCUP) es una herramienta independiente que permite a proveedores de software independientes o desarrolladores de aplicaciones de línea de negocio administrar actualizaciones personalizadas. Estas incluyen las que tienen dependencias, como controladores y agrupaciones de actualizaciones.

Para obtener más información, vea [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).



##  <a name="BKMK_SUPInstallation"></a> Planeamiento de la instalación de puntos de actualización de software  

Esta sección incluye los subtemas siguientes:  
- [Requisitos del punto de actualización de software](#BKMK_SUPSystemRequirements)
- [Planear la instalación de WSUS](#BKMK_PlanningForWSUS)
- [Configurar firewalls](#BKMK_ConfigureFirewalls)  


Esta sección proporciona información acerca de los pasos para planear y preparar correctamente la instalación de los puntos de actualización de software. Antes de crear un rol de sistema de sitio para el punto de actualización de software en Configuration Manager, hay varios requisitos que debe tener en cuenta. Los requisitos específicos dependen de la infraestructura de Configuration Manager. Al configurar el punto de actualización de software para comunicarse a través de HTTPS, es especialmente importante revisar esta sección. Los servidores habilitados para HTTPS requieren pasos adicionales para funcionar correctamente.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requisitos del punto de actualización de software  

Instale el rol de punto de actualización en un sitio del sistema que cumpla los requisitos mínimos de WSUS y las configuraciones compatibles con sistema de sitio de Configuration Manager.  

-   Para obtener más información sobre los requisitos mínimos para el rol de servidor WSUS en Windows Server, consulte [Review considerations and system requirements (Revisar consideraciones iniciales y requisitos del sistema)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#BKMK_1.1).  

-   Para más información sobre las configuraciones admitidas para los sistemas de sitio de Configuration Manager, consulte [Requisitos previos del sitio y el sistema de sitio](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


###  <a name="BKMK_PlanningForWSUS"></a> Planear la instalación de WSUS  

Instale una versión compatible de WSUS en todos los servidores de sistema de sitio configurados para el rol de punto de actualización de software. Cuando no instale el punto de actualización de software en el servidor del sitio, debe instalar la consola de administración de WSUS en el servidor de sitio. Este componente permite que el servidor de sitio se comunique con el WSUS que se ejecuta en el punto de actualización de software.  

Cuando use WSUS en Windows Server 2012 o posterior, debe configurar permisos adicionales para permitir que el componente **Administrador de configuración de WSUS** de Configuration Manager se conecte a WSUS. Este componente realiza comprobaciones de estado periódicas. Elija una de las siguientes opciones para configurar los permisos necesarios:  

-   Agregar la cuenta **SYSTEM** al grupo **Administradores de WSUS**  

-   Agregar la cuenta **NT AUTHORITY\SYSTEM** como un usuario de la base de datos WSUS (SUSDB). Configurar un valor mínimo de la pertenencia al rol de base de datos webService.  
  
Para obtener más información acerca de cómo instalar WSUS en Windows Server, consulte [Install the WSUS Server Role (Instalar el rol de servidor de WSUS)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Cuando instale más de un punto de actualización de software en un sitio primario, utilice la misma base de datos de WSUS para cada punto de actualización de software del mismo bosque de Active Directory. Compartir la misma base de datos mejora el rendimiento cuando los clientes cambian a un nuevo punto de actualización de software. Para obtener más información, vea [Usar una base de datos WSUS compartida para los puntos de actualización de software](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb).  


####  <a name="BKMK_CustomWebSite"></a> Configurar WSUS para usar un sitio web personalizado  
Al instalar WSUS, tiene la opción de utilizar el sitio web de IIS predeterminado existente o crear un sitio web de WSUS personalizado. Cree un sitio web personalizado para WSUS para que IIS hospede los servicios WSUS en un sitio web virtual dedicado. En caso contrario, comparte el mismo sitio web que usan otros sistemas de sitio o aplicaciones de Configuration Manager. Esta configuración es especialmente necesaria cuando se instala el rol de punto de actualización de software en el servidor de sitio. Cuando se ejecuta WSUS en Windows Server 2012 o posterior, WSUS se configura de forma predeterminada para usar el puerto 8530 para HTTP y el puerto 8531 para HTTPS. Especifique estos puertos al crear el punto de actualización de software en un sitio.  


####  <a name="BKMK_WSUSInfrastructure"></a> Usar una infraestructura de WSUS existente  
Seleccione un servidor WSUS que estuviera activo en su entorno antes de instalar Configuration Manager como un punto de actualización de software. Cuando configure el punto de actualización de software, especifique la configuración de sincronización. Configuration Manager se conecta con el servidor WSUS que se ejecuta en el servidor de punto de actualización de software y configura WSUS con los mismos ajustes. 

Antes de configurar el servidor como un punto de actualización de software, compare su configuración de productos y clasificaciones con la configuración de Configuration Manager. Si sincroniza el servidor WSUS existente antes de configurarlo como un punto de actualización de software y las listas de productos y clasificaciones son diferentes, sincroniza todos los metadatos de actualizaciones de software independientemente de los valores configurados. Este comportamiento tiene como consecuencia metadatos de las actualizaciones de software inesperados en la base de datos del sitio. 

Experimentará el mismo comportamiento si agrega productos o clasificaciones directamente en la consola de administración de WSUS y después inicia inmediatamente una sincronización. De forma predeterminada, cada hora Configuration Manager se conecta al WSUS y restablece las opciones que se modificaron fuera de Configuration Manager. Las actualizaciones de software que no cumplan con los productos y las clasificaciones especificados en la configuración de sincronización se establecen como expiradas. Luego, se quitan de la base de datos del sitio.  

Cuando un servidor WSUS se configura como un punto de actualización de software, ya no es posible utilizarlo como un servidor WSUS independiente. Si necesita un servidor WSUS independiente no administrado por Configuration Manager, configúrelo en un servidor diferente.  

####  <a name="BKMK_WSUSAsReplica"></a> Configurar WSUS como un servidor de réplica  
Cuando se agrega el rol de punto de actualización de software en un servidor de sitio primario, no se puede utilizar un servidor WSUS que esté configurado como una réplica. Cuando el servidor WSUS está configurado como una réplica, Configuration Manager no puede configurar el servidor WSUS, y la sincronización de WSUS tampoco se puede llevar a cabo. El primer punto de actualización de software que se instala en un sitio primario es el punto de actualización de software predeterminado. Los puntos de actualización de software adicionales del sitio se configuran como réplicas del punto de actualización de software predeterminado.  

####  <a name="BKMK_WSUSandSSL"></a> Decidir si se va a configurar WSUS para usar SSL  
Use el protocolo SSL para proteger el punto de actualización de software. WSUS utiliza SSL para autenticar en el servidor WSUS los equipos cliente y los servidores WSUS que siguen en la cadena. WSUS también utiliza SSL para cifrar los metadatos de las actualizaciones de software. Si decide proteger WSUS con SSL, prepare el servidor WSUS antes de instalar el punto de actualización de software. Para obtener más información, vea el artículo [Configure SSL on the WSUS server (Configurar SSL en el servidor WSUS)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) en la documentación de WSUS. 

Cuando instala y configura el punto de actualización de software, debe seleccionar la opción para **Habilitar las comunicaciones SSL para el servidor WSUS**. De lo contrario, Configuration Manager configura WSUS para que no use SSL. Cuando habilite SSL en un punto de actualización de software, configure también los puntos de actualización de software en sitios secundarios para que usen SSL.  


###  <a name="BKMK_ConfigureFirewalls"></a> Configurar firewalls  

El punto de actualización de software en un sitio de administración central de Configuration Manager se comunica con WSUS en el punto de actualización de software. WSUS se comunica con el origen de sincronización para sincronizar los metadatos de actualizaciones de software. Los puntos de actualización de software de un sitio secundario se comunican con el punto de actualización de software del sitio primario. Cuando hay más de un punto de actualización de software en un sitio primario, los puntos de actualización de software adicionales se comunican con el punto de actualización de software predeterminado. El rol predeterminado es el primer punto de actualización de software que está instalado en el sitio.  

Es posible que deba configurar el firewall para permitir el tráfico HTTP o HTTPS que WSUS utiliza en los escenarios siguientes: 
- Entre el punto de actualización de software e Internet
- Entre un punto de actualización de software y su origen de sincronización ascendente
- Entre puntos de actualización de software adicionales  

La conexión a Microsoft Update siempre está configurada para utilizar el puerto 80 para HTTP y el puerto 443 para HTTPS. Use un puerto personalizado para la conexión del WSUS en el punto de actualización de software de un sitio secundario al WSUS que se ejecuta en el punto de actualización de software del sitio primario. Si la directiva de seguridad no permite la conexión, use el método de sincronización de exportación e importación. Para más información, vea la sección [Origen de la sincronización](#BKMK_SyncSource) en este artículo. Para obtener más información sobre los puertos que usa WSUS, vea [Cómo determinar la configuración del puerto que usa WSUS](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Restringir el acceso a dominios específicos  
Si su organización no permite que los puertos y protocolos estén abiertos a todas las direcciones del firewall entre el punto de actualización de software activo e Internet, restrinja el acceso a los siguientes dominios para que WSUS y Actualizaciones automáticas se puedan comunicar con Microsoft Update:  

-   `http://windowsupdate.microsoft.com`  

-   `http://*.windowsupdate.microsoft.com`  

-   `https://*.windowsupdate.microsoft.com`  

-   `http://*.update.microsoft.com`  

-   `https://*.update.microsoft.com`  

-   `http://*.windowsupdate.com`  

-   `http://download.windowsupdate.com`  

-   `http://download.microsoft.com`  

-   `http://*.download.windowsupdate.com`  

-   `http://test.stats.update.microsoft.com`  

-   `http://ntservicepack.microsoft.com`  

Podría ser necesario agregar las siguientes direcciones al firewall que se encuentra entre los dos sistemas de sitio en los casos siguientes: 
- Si los sitios secundarios tienen un punto de actualización de software 
- Si hay un punto de actualización de software basado en Internet activo remoto en un sitio

 **Punto de actualización de software del sitio secundario**  

-   `http://<FQDN for software update point on child site>`  

-   `https://<FQDN for software update point on child site>`  

-   `http://<FQDN for software update point on parent site>`  

-   `https://<FQDN for software update point on parent site>`  



##  <a name="BKMK_SyncSettings"></a> Planear la configuración de sincronización  

Esta sección incluye los subtemas siguientes:  
- [Origen de la sincronización](#BKMK_SyncSource)
- [Programación de la sincronización](#BKMK_SyncSchedule)
- [Clasificaciones de actualizaciones](#BKMK_UpdateClassifications)
- [Productos](#BKMK_UpdateProducts)
- [Reglas de sustitución](#BKMK_SupersedenceRules)
- [Idiomas](#BKMK_UpdateLanguages)  


La sincronización de las actualizaciones de software de Configuration Manager descargan los metadatos de las actualizaciones de software en función de los criterios que se configuren. El sitio de nivel superior de la jerarquía sincroniza las actualizaciones de software desde Microsoft Update. Tiene la opción de configurar el punto de actualización de software en el sitio de nivel superior para la sincronización con un servidor WSUS existente, no en la jerarquía de Configuration Manager. Los sitios primarios secundarios sincronizan los metadatos de las actualizaciones de software desde el punto de actualización de software del sitio de administración central. Antes de instalar y configurar un punto de actualización de software, utilice esta sección para planear la configuración de sincronización.  


###  <a name="BKMK_SyncSource"></a> Origen de la sincronización  

En la configuración del origen de la sincronización del punto de actualización de software se especifica la ubicación desde la cual el punto de actualización de software recupera los metadatos de las actualizaciones de software. También se especifica si se crean eventos de informe de WSUS durante el proceso de sincronización.  

-   **Origen de sincronización**: de forma predeterminada, el punto de actualización de software del sitio de nivel superior configura el origen de sincronización para Microsoft Update. Tiene la opción de sincronizar el sitio de nivel superior con un servidor WSUS existente. El punto de actualización de software de un sitio primario secundario configura el origen de la sincronización como el punto de actualización de software del sitio de administración central.  

    -  El primer punto de actualización de software que se instala en un sitio primario, que es el punto de actualización de software predeterminado, se sincroniza con el sitio de administración central. Los puntos de actualización de software adicionales del sitio primario se sincronizan con el punto de actualización de software predeterminado del sitio primario.  

    - Si un punto de actualización de software se desconecta de Microsoft Update o del servidor de actualización que precede en la cadena, configure el origen de la sincronización de manera que no se realice la sincronización con un origen de la sincronización configurado. En su lugar, configúrelo para que se utilice la función de exportación e importación de la herramienta **WSUSUtil** para sincronizar las actualizaciones de software. Para obtener más información, consulte [Sincronizar actualizaciones de software desde un punto de actualización de software desconectado](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventos de informe de WSUS:** El Agente de Windows Update de los equipos cliente puede crear mensajes de evento para la generación de informes de WSUS. Configuration Manager no usa estos eventos. Por lo tanto, la opción **No crear eventos de informe de WSUS** está activada de forma predeterminada. Cuando no se crean estos eventos, el único momento en que el cliente se debe conectar al servidor WSUS es durante los exámenes de cumplimiento y de evaluación de las actualizaciones de software. Si se necesitan estos eventos para la generación de informes fuera de Configuration Manager, es necesario modificar esta configuración para crear eventos de informe de WSUS.  


###  <a name="BKMK_SyncSchedule"></a> Programación de la sincronización  

Solo se puede configurar la programación de sincronización en el punto de actualización de software del sitio de nivel superior de la jerarquía de Configuration Manager. Cuando se configura la programación de sincronización, el punto de actualización de software se sincroniza con el origen de la sincronización en la fecha y a la hora especificadas. La programación personalizada permite sincronizar las actualizaciones de software para optimizar su entorno. Tenga en cuenta las exigencias de rendimiento del servidor WSUS, el servidor de sitio y la red. Por ejemplo, a las 2:00 una vez por semana. Como alternativa, inicie manualmente la sincronización en el sitio de nivel superior mediante la acción **Sincronizar actualizaciones de software** de los nodos **Todas las actualizaciones de software** o **Grupos de actualizaciones de software** de la consola de Configuration Manager.  

> [!TIP]  
>  Programe la sincronización de las actualizaciones de software para que se ejecuten en un momento adecuado para su entorno. Un escenario habitual es configurar la programación de la sincronización para que se ejecute poco tiempo después del lanzamiento de las actualizaciones de software periódicas de Microsoft los segundos martes de cada mes. Este evento se conoce habitualmente como *Patch Tuesday*. Si utiliza Configuration Manager para entregar actualizaciones de motor y de definición de Endpoint Protection y Windows Defender, considere la posibilidad de establecer la programación de sincronización para que se ejecute a diario.  

Una vez que el punto de actualización de software se sincroniza correctamente, envía una solicitud de sincronización a los sitios secundarios. Si tiene puntos de actualización de software adicionales en un sitio primario, envía una solicitud de sincronización a cada punto de actualización de software. Este proceso se repite en cada sitio de la jerarquía.  


###  <a name="BKMK_UpdateClassifications"></a> Clasificaciones de actualizaciones  

Cada actualización de software se define con una clasificación de actualización que facilita la organización de los distintos tipos de actualizaciones. Durante el proceso de sincronización, el sitio sincroniza los metadatos de las actualizaciones de software para las clasificaciones especificadas. 

Configuration Manager admite la sincronización de las siguientes clasificaciones de actualización:  

-   **Actualizaciones críticas**: una actualización de amplia distribución para un problema específico que resuelve un error crítico no relacionado con la seguridad.  

-   **Actualizaciones de definiciones**: una actualización para un archivo de definición de virus u otros.  

-   **Feature Packs**: nuevas características de producto que se distribuyen fuera de una versión del producto y que normalmente se incluyen en la siguiente versión completa del producto.  

-   **Actualizaciones de seguridad**: una actualización de amplia distribución para un problema específico del producto relacionado con la seguridad.  

-   **Service Pack**: un conjunto acumulativo de revisiones correspondientes a un SO o una aplicación. Estas revisiones incluyen actualizaciones de seguridad, actualizaciones críticas y actualizaciones de software.  

-   **Herramientas**: una utilidad o característica que ayuda a realizar una o varias tareas.  

-   **Paquete acumulativo de actualizaciones**: conjunto acumulativo de revisiones que se recopilan para facilitar la implementación. Estas revisiones incluyen actualizaciones de seguridad, actualizaciones críticas y actualizaciones de software. Un paquete acumulativo de revisiones suele relacionarse, por lo general, con un área específica; por ejemplo, un componente del producto o de la seguridad.  

-   **Actualizaciones**: una actualización de una aplicación o un archivo que está instalado actualmente.  

-   **Actualizaciones**: una actualización de características a una nueva versión de Windows 10.  

Configure las clasificaciones de actualizaciones solo en el sitio de nivel superior. Las clasificaciones de actualizaciones no se configuran en el punto de actualización de software de los sitios secundarios, porque los metadatos de las actualizaciones de software se replican desde el sitio de nivel superior. Al seleccionar las clasificaciones de actualizaciones, tenga en cuenta que cuantas más clasificaciones seleccione, más tiempo tarda la sincronización de los metadatos de las actualizaciones de software.  

> [!WARNING]  
>  Como práctica recomendada, desactive todas las clasificaciones antes de sincronizar por primera vez. Después de la sincronización inicial, seleccione las clasificaciones deseadas y luego vuelva a ejecutar la sincronización.  


###  <a name="BKMK_UpdateProducts"></a> Productos  

Los metadatos de cada actualización de software definen uno o varios productos a los que corresponde la actualización. Un producto es una edición específica de una aplicación o un sistema operativo. Un ejemplo de un producto es Microsoft Windows 10. Una familia de productos es el sistema operativo o la aplicación de base de los cuales se derivan los productos individuales. Un ejemplo de una familia de productos es Microsoft Windows, de la que Windows 10 y Windows Server 2016 son miembros. Seleccione una familia de productos o productos individuales dentro de una familia de productos.  

Cuando las actualizaciones de software son aplicables a varios productos y al menos se selecciona uno de ellos para sincronización, todos los productos aparecerán en la consola de Configuration Manager, aunque algunos no se hayan seleccionado. Por ejemplo, solo selecciona el producto Windows Server 2012. Si una actualización de software se aplica a Windows Server 2012 y Windows Server 2012 Datacenter Edition, ambos productos se encuentran en la base de datos del sitio.  

Configure las opciones del producto solo en el sitio de nivel superior. Las opciones del producto no se configuran en el punto de actualización de software para los sitios secundarios, porque los metadatos de las actualizaciones de software se replican desde el sitio de nivel superior. Cuantos más productos seleccione, más tiempo tomará sincronizar los metadatos de las actualizaciones de software.  

> [!IMPORTANT]  
>  Configuration Manager almacena una lista de productos y familias de productos entre los que elige cuando instala por primera vez el punto de actualización de software. Los productos y las familias de productos que se publicaron después del lanzamiento de Configuration Manager no están disponibles para seleccionarlos hasta que se complete la sincronización. El proceso de sincronización actualiza la lista de productos disponibles y las familias de productos desde las que puede elegir. Desactive todos los productos antes de sincronizar por primera vez las actualizaciones de software. Después de la sincronización inicial, seleccione los productos deseados y luego vuelva a ejecutar la sincronización.  


###  <a name="BKMK_SupersedenceRules"></a> Reglas de sustitución  

Por lo general, una actualización de software que sustituye a otra actualización de software realiza una o varias de las siguientes acciones:  

-   Mejora o actualiza la revisión proporcionada por una o varias de las actualizaciones publicadas anteriormente.  

-   Mejora la eficacia del paquete de archivos de actualización sustituidos, que se instala en los clientes si se aprueba la actualización para la instalación. Por ejemplo, la actualización reemplazada puede contener archivos que ya no correspondan a la corrección o a los sistemas operativos que la nueva actualización admite. Esos archivos no se incluyen en el paquete de archivos de reemplazo de la actualización.  

-   Actualiza las versiones más recientes de un producto. En otras palabras, actualiza las versiones que ya no se aplican a las versiones o configuraciones más antiguas de un producto. Las actualizaciones también pueden sustituir a otras actualizaciones si se han realizado modificaciones para ampliar la compatibilidad de idioma. Por ejemplo, una revisión posterior de una actualización de un producto para Microsoft Office puede quitar la compatibilidad para un sistema operativo más antiguo, pero podría agregar compatibilidad adicional para nuevos idiomas en la versión de actualización inicial.  

En las propiedades para el software del punto de actualización, especifique que las actualizaciones de software sustituidas expiran inmediatamente. Esta configuración evita que se incluyan en nuevas implementaciones. También marca las implementaciones existentes para indicar que contienen una o varias actualizaciones de software expiradas. O bien, especifique un período de tiempo antes de que las actualizaciones de software sustituidas expiren. Esta acción le permite continuar con las implementaciones. 

Tenga en cuenta los siguientes escenarios en los que puede que necesite implementar una actualización de software sustituida:  

-   Una actualización de software de reemplazo admite solo las versiones más recientes de un sistema operativo. Algunos de los equipos cliente ejecutan versiones anteriores del sistema operativo.  

-   Una actualización de software de remplazo tiene una aplicabilidad más restringida que la actualización de software que reemplaza. Este comportamiento la haría inapropiada para algunos clientes.  

-   Si una actualización de software de sustitución no se aprobó para su implementación en el entorno de producción.  

    > [!NOTE]  
    > Cuando Configuration Manager establece una actualización de software reemplazada en estado **Expirado**, no establece la actualización en **Rechazado** en WSUS. En cambio, cuando se ejecuta la tarea de limpieza de WSUS, las actualizaciones configuradas en el estado **Expirado** en Configuration Manager se establecen en un estado de **Rechazado** en el servidor de WSUS. Por lo tanto, el agente de Windows Update de los equipos ya no buscará estas actualizaciones. Los clientes siguen buscando una actualización caducada hasta que se ejecute la tarea de limpieza. Para obtener más información sobre la tarea de limpieza de WSUS, consulte [Mantenimiento de las actualizaciones de software](/sccm/sum/deploy-use/software-updates-maintenance).  


###  <a name="BKMK_UpdateLanguages"></a> Idiomas  

La configuración de idioma para el punto de actualización de software le permite configurar: 
- Los idiomas para los que se sincronizan las actualizaciones de software de los detalles de resumen (metadatos de actualizaciones de software)  
- Los idiomas de los archivos de actualización de software que se descargan para las actualizaciones de software  

#### <a name="software-update-file"></a>Archivo de actualización de software  
Configure los idiomas para la opción **Archivo de actualización de software** estableciendo las propiedades para el punto de actualización de software. Esta configuración proporciona los idiomas predeterminados que están disponibles al descargar las actualizaciones de software en un sitio. Modifique los idiomas seleccionados de manera predeterminada cada vez que se van a descargar o implementar las actualizaciones de software. Durante el proceso de descarga, los archivos de actualización de software para los idiomas configurados se descargan en la ubicación de origen del paquete de implementación, si los archivos de actualización de software están disponibles en el idioma seleccionado. Después, se copian a la biblioteca de contenido en el servidor de sitio. Luego, se distribuyen a los puntos de distribución que están configurados para el paquete.  

Configure la opción de idioma del archivo de configuración de software con los idiomas que se utilizan con más frecuencia en el entorno. Por ejemplo, los clientes de su sitio usan principalmente inglés y japonés para Windows o aplicaciones. Hay algunos idiomas adicionales que se usan en el sitio. Seleccione solo inglés y japonés en la columna **Archivo de actualización de software** al descargar o implementar la actualización de software. Esta acción le permite utilizar la configuración predeterminada en la página **Selección de idioma** de los asistentes de implementación y descarga. Esta acción también impide la descarga de archivos de actualización no necesarios. Configure esta opción en cada punto de actualización de software de la jerarquía de Configuration Manager.  

#### <a name="summary-details"></a>Detalles de resumen  
Durante el proceso de sincronización, se actualiza la información de detalles de resumen (metadatos de las actualizaciones de software) para buscar actualizaciones de software en los idiomas especificados. Los metadatos proporcionan información sobre la actualización de software, por ejemplo:
- Nombre
- Descripción
- Productos compatibles con la actualización
- Clasificación de actualizaciones
- Identificador de artículo
- Dirección URL de descarga
- Reglas de aplicabilidad

Configure las opciones de los detalles de resumen solo en el sitio de nivel superior. Los detalles de resumen no se configuran en el punto de actualización de software en los sitios secundarios porque los metadatos de actualizaciones de software se replican desde el sitio de administración central mediante una replicación basada en archivos. Al seleccionar los idiomas de los detalles de resumen, seleccione solo los idiomas que necesita en el entorno. Cuantos más idiomas seleccione, más tiempo tomará sincronizar los metadatos de las actualizaciones de software. Configuration Manager muestra los metadatos de las actualizaciones de software en la configuración regional del sistema operativo en el que se ejecuta la consola de Configuration Manager. Si las propiedades localizadas de las actualizaciones de software no están disponibles en la configuración regional de este sistema operativo, la información de las actualizaciones de software se muestra en inglés.  

> [!IMPORTANT]  
>  Seleccione todos los idiomas de los detalles de resumen que necesita. Cuando el punto de actualización de software del sitio de nivel superior se sincroniza con el origen de la sincronización, los idiomas de los detalles de resumen seleccionados determinan los metadatos de las actualizaciones de software que recupera. Si modifica los idiomas de los detalles de resumen después de que la sincronización se haya ejecutado al menos una vez, recupera los metadatos de las actualizaciones de software para los idiomas de los detalles de resumen modificados solo para las actualizaciones de software nuevas o actualizadas. Las actualizaciones de software ya sincronizadas no se actualizan con los nuevos metadatos en los idiomas modificados, salvo que se produzca un cambio en la actualización de software en el origen de la sincronización.  



##  <a name="BKMK_MaintenanceWindow"></a> Planear una ventana de mantenimiento de actualizaciones de software  

Agregue una ventana de mantenimiento dedicada a la instalación de actualizaciones de software. Esta acción le permite configurar una ventana de mantenimiento general y una ventana de mantenimiento diferente para las actualizaciones de software. Cuando configure una ventana de mantenimiento general y una ventana de mantenimiento de actualizaciones de software, los clientes solo instalan las actualizaciones de software durante la ventana de mantenimiento de actualizaciones de software. Para obtener más información sobre las ventanas de mantenimiento, consulte [Cómo utilizar las ventanas de mantenimiento](../../core/clients/manage/collections/use-maintenance-windows.md).  



##  <a name="BKMK_RestartOptions"></a> Opciones de reinicio para clientes de Windows 10 después de la instalación de las actualizaciones de software

Cuando se implementa y se instala una actualización de software que requiere un reinicio con Configuration Manager, el cliente programa un reinicio pendiente y muestra un cuadro de diálogo de reinicio.

Cuando hay un reinicio pendiente para una actualización de software de Configuration Manager, la opción para **Actualizar y reiniciar** y **Actualizar y apagar** está disponible en los equipos de Windows 10 en las opciones de energía de Windows. Después de utilizar una de estas opciones, tras reiniciar el equipo, no se mostrará el cuadro de diálogo de reinicio.



## <a name="next-steps"></a>Pasos siguientes
Cuando haya planificado las actualizaciones de software, consulte [Preparación para la administración de actualizaciones de software](../get-started/prepare-for-software-updates-management.md).  

Para obtener más información sobre cómo administrar Windows como servicio, vea [Aspectos básicos de Configuration Manager como servicio y de Windows como servicio](/sccm/core/understand/configuration-manager-and-windows-as-service).
