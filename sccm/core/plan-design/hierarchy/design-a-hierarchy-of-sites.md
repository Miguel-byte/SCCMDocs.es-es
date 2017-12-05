---
title: "Diseño de una jerarquía de sitios "
titleSuffix: Configuration Manager
description: "Conozca las topologías disponibles y las opciones de administración de System Center Configuration Manager para poder planear la jerarquía del sitio."
ms.custom: na
ms.date: 8/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: "22"
caps.handback.revision: "0"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: f4bfad43e6ed47b8b69ba35865a3a36b833723c5
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Diseñar una jerarquía de sitios para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Antes de instalar el primer sitio de una nueva jerarquía de System Center Configuration Manager, es aconsejable comprender las topologías disponibles para Configuration Manager, los tipos de sitios disponibles y sus relaciones entre sí, y el ámbito de administración que proporciona cada tipo de sitio.
Posteriormente, después de considerar las opciones de administración de contenido que pueden reducir el número de sitios que debe instalar, puede planear una topología que satisfaga de forma eficaz sus necesidades de negocio actuales y que más tarde se pueda expandir para administrar el crecimiento futuro.  

Al realizar la planificación, tenga en cuenta las limitaciones para agregar sitios adicionales a una jerarquía o a un sitio independiente:
-   Puede instalar un nuevo sitio primario por debajo de un sitio de administración central, hasta el [número admitido de sitios primarios](/sccm/core/plan-design/configs/size-and-scale-numbers) de la jerarquía.
-   Puede [expandir un sitio primario independiente para instalar un nuevo sitio de administración central](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), de modo que pueda instalar entonces sitios primarios adicionales.
-   Puede instalar nuevos sitios secundarios debajo de un sitio primario, hasta los [límites admitidos para el sitio primario](/sccm/core/plan-design/configs/size-and-scale-numbers) y la jerarquía general.
-   No se puede agregar un sitio instalado previamente a una jerarquía existente para combinar dos sitios independientes. Solo se admite la instalación de nuevos sitios a una jerarquía de sitios existente.


> [!NOTE]
> Al planear una nueva instalación de Configuration Manager, tenga en cuenta las [notas de la versión]( /sccm/core/servers/deploy/install/release-notes) que detallan los problemas actuales en las versiones activas. Las notas de la versión se aplican a todas las ramas de Configuration Manager.  Pero cuando use la [rama Technical Preview]( /sccm/core/get-started/technical-preview), encontrará problemas que afectan solamente a esa rama en la documentación de cada versión de Technical Preview.  

##  <a name="bkmk_topology"></a> Topología de la jerarquía  
 Las topologías de las jerarquías van desde un único sitio principal independiente hasta un grupo de sitios principales y secundarios conectados con un sitio de administración central en el sitio de nivel superior (capa superior) de la jerarquía.   El impulsor clave del tipo y del número de sitios que use en una jerarquía suele ser el número y tipo de dispositivos que debe admitir, como se muestra a continuación:   

 **Sitio primario independiente:** use un sitio primario independiente si este puede admitir la administración de todos los dispositivos y usuarios (consulte [Sizing and scale numbers](/sccm/core/plan-design/configs/size-and-scale-numbers) [Números de tamaño y escala]). Esta también es la topología adecuada cuando las diferentes ubicaciones geográficas de su empresa pueden atenderse correctamente mediante un solo sitio principal.  Para que sea más fácil administrar el tráfico de red, puede usar puntos de administración preferidos y una infraestructura de contenido planeada cuidadosamente (vea [Conceptos básicos de la administración de contenido en System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 Entre las ventajas de esta topología cabe destacar:  

-   Simplificación del trabajo administrativo.  

-   Simplificación de la asignación del sitio cliente y la detección de servicios y recursos disponibles.  

-   Eliminación de posibles retrasos introducidos por la replicación de base de datos entre sitios.

-   Opción para expandir una jerarquía primaria independiente hacia una jerarquía más grande con un sitio de administración central. Esto le permite instalar nuevos sitios primarios para expandir la escala de la implementación.  


**Sitio de administración central con uno o más sitios principales secundarios:** Use esta topología cuando necesite más de un sitio principal para admitir la administración de todos los dispositivos y usuarios.  Es obligatorio cuando necesita usar más de un solo sitio primario. Entre las ventajas de esta topología cabe destacar:  


-   Admite hasta 25 sitios primarios, lo que le permite extender la escala de la jerarquía.  

-   Siempre tendrá que usar el sitio de administración central (a menos que vuelva a instalar los sitios). Esta opción es permanente. No se puede separar un sitio primario secundario para que convertirlo en sitio primario independiente.

 Las secciones siguientes pueden ayudarle a entender cuándo se debe utilizar un sitio específico o una opción de administración de contenido en lugar de un sitio adicional.  

##  <a name="BKMK_ChooseCAS"></a> Determinar cuándo usar un sitio de administración central  
 Utilice un sitio de administración central para configurar toda la jerarquía y supervisar todos los sitios y objetos de la jerarquía. Este tipo de sitio no administra directamente los clientes, sino que coordina la replicación de datos entre sitios, que incluye la configuración de sitios y clientes en toda la jerarquía.  

**La siguiente información puede ayudarle a decidir cuándo instalar un sitio de administración central:**  

-   El sitio de administración central es el sitio de nivel superior de una jerarquía.  

-   Cuando se configura una jerarquía que tiene más de un sitio primario, debe instalar un sitio de administración central. Si se necesitan dos o más sitios primarios inmediatamente, instale primero el sitio de administración central. Si ya tiene un sitio primario y desea instalar un sitio de administración central, debe [expandir el sitio primario independiente](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) para instalar el sitio de administración central.

-   El sitio de administración central admite sólo sitios primarios como sitios secundarios.  

-   El sitio de administración central no puede tener clientes asignados a él.  

-   El sitio de administración central no admite roles de sistema de sitio que admitan clientes directamente, como puntos de administración y puntos de distribución.  

-   Puede administrar todos los clientes de la jerarquía y realizar las tareas de administración de cualquier sitio secundario cuando use una consola de Configuration Manager conectada al sitio de administración central. Esto puede incluir la instalación de puntos de administración o de otros roles de sistema de sitio en sitios primarios secundarios o en sitios secundarios.  

-   Cuando se utiliza un sitio de administración central, este sitio es el único lugar donde puede ver datos de sitio desde todos los sitios de la jerarquía. Estos datos incluyen información como mensajes de estado y datos de inventario.  

-   Puede configurar operaciones de detección en toda la jerarquía desde el sitio de administración central mediante la asignación de métodos de detección para que se ejecuten en sitios individuales.  

-   Puede administrar la seguridad en toda la jerarquía mediante la asignación de roles de seguridad diferentes, ámbitos de seguridad y colecciones a usuarios administrativos distintos. Estas configuraciones se aplican en cada sitio de la jerarquía.  

-   Puede configurar la replicación de archivos y replicación de bases de datos para controlar la comunicación entre los sitios de la jerarquía. Esto incluye la programación de replicación de bases de datos para los datos del sitio y la administración del ancho de banda para la transferencia entre sitios de datos basados en archivos.  

##  <a name="BKMK_ChoosePriimary"></a> Determinar cuándo usar un sitio primario  
 Utilice los sitios primarios para administrar clientes. Puede instalar un sitio primario como sitio primario secundario en un sitio de administración central o como el primer sitio de una nueva jerarquía. Un sitio primario que se instala como el primer sitio de la jerarquía crea un sitio primario independiente. Los sitios primarios secundarios y los sitios primarios independientes admiten sitios secundarios como sitios secundarios del sitio primario.  

 Considere la posibilidad de utilizar un sitio primario por alguna de las siguientes razones:  

-   Para administrar dispositivos y usuarios.  

-   Para aumentar el número dispositivos que puede administrar con una sola jerarquía.  

-   Para proporcionar un punto adicional de conectividad para la administración de la implementación.  

-   Para satisfacer los requisitos de administración organizativa. Por ejemplo, puede instalar un sitio primario en una ubicación remota para administrar la transferencia de contenido de implementación a través de una red de ancho de banda bajo. Pero con System Center Configuration Manager puede usar opciones para limitar el ancho de banda de red que se usa al transferir datos a un punto de distribución. Esta capacidad de administración de contenido puede sustituir la necesidad de instalar sitios adicionales.  


**La siguiente información puede ayudarle a decidir cuándo instalar un sitio primario:**  

-   Un sitio primario puede ser un sitio primario independiente o un sitio primario secundario en una jerarquía más grande. Si un sitio primario es miembro de una jerarquía con un sitio de administración central, los sitios utilizan la replicación de base de datos para replicar datos entre sitios. A menos que precise admitir un número de clientes y dispositivos superior al compatible con un solo sitio primario, considere la posibilidad de instalar un sitio primario independiente.  Después de instalar un sitio primario independiente, puede expandirlo para que informe a un nuevo sitio de administración central a fin de escalar la implementación.  

-   Un sitio primario admite un solo sitio de administración central como sitio principal.  

-   Un sitio primario solo admite sitios secundarios como sitios secundarios y también puede admitir varios sitios secundarios.  

-   Los sitios primarios son responsables de procesar todos los datos de cliente de los clientes asignados.  

-   Los sitios primarios usan la replicación de base de datos para comunicarse directamente con su sitio de administración central (esto se configura automáticamente cuando se instala un nuevo sitio).  

##  <a name="BKMK_ChooseSecondary"></a> Determinar cuándo usar un sitio secundario  
 Utilice sitios secundarios para administrar la transferencia de contenido de implementación y datos de cliente a través de redes de ancho de banda bajo.  

 Es posible administrar un sitio secundario desde un sitio de administración central o desde el sitio primario principal directo del sitio secundario. Los sitios secundarios deben estar conectados a un sitio primario y no es posible moverlos a un sitio primario diferente sin desinstarlarlos y volverlos a instalar a continuación como un sitio secundario debajo del nuevo sitio primario.

Sin embargo, es posible distribuir contenido entre dos sitios secundarios del mismo nivel para facilitar la administración de la replicación basada en archivos de contenido de implementación. Para transferir datos de cliente a un sitio primario, el sitio secundario utiliza replicación basada en archivos. Un sitio secundario también utiliza replicación de base de datos para comunicarse con su sitio primario principal.  

 Considere la posibilidad de instalar un sitio secundario si se cumple alguna de las condiciones siguientes:  

-   No necesita un punto local de conectividad para un usuario administrativo.  

-   Debe administrar la transferencia de contenido de implementación a los sitios situados más abajo en la jerarquía.  

-   Debe administrar la información de cliente que se envía a sitios situados más arriba en la jerarquía.  

 Si no desea instalar un sitio secundario y tiene clientes en ubicaciones remotas, considere la posibilidad de usar Windows BranchCache o instalar puntos de distribución habilitados para control de ancho de banda y programación. También puede usar estas opciones de administración de contenido con o sin sitios secundarios, y pueden ayudarle a reducir el número de sitios y servidores que debe instalar. Para obtener información sobre las opciones de administración de contenido en Configuration Manager, consulte [Determinar si se debe instalar un sitio o usar opciones de administración de contenido](#BKMK_ChooseSecondaryorDP).  


**La siguiente información puede ayudarle a decidir cuándo instalar un sitio secundario:**  

-   Los sitios secundarios instalan automáticamente SQL Server Express durante la instalación del sitio si una instancia local de SQL Server no está disponible.  

-   La instalación del sitio secundario se inicia desde la consola de Configuration Manager, en lugar de ejecutar el programa de instalación directamente en un equipo.  

-   Los sitios secundarios usan un subconjunto de la información en la base de datos del sitio, que reduce la cantidad de datos que se replican mediante la replicación de base de datos entre el sitio primario principal y el sitio secundario.  

-   Los sitios secundarios admiten la distribución de contenido basado en archivos a otros sitios secundarios que tienen un sitio primario principal común.  

-   Las instalaciones de sitio secundario implementan automáticamente un punto de administración y un punto de distribución que se encuentran en el servidor de sitio secundario.  

##  <a name="BKMK_ChooseSecondaryorDP"></a> Determinar cuándo usar las opciones de administración de contenido  
 Si tiene clientes en ubicaciones de red remotas, considere el uso de una o varias opciones de administración de contenido en lugar de un sitio primario o secundario. A menudo, puede eliminar la necesidad de instalar un sitio si utiliza Windows BranchCache, configura los puntos de distribución para el control de ancho de banda o copia manualmente el contenido en puntos de distribución (contenido preconfigurado).  


**Considere la posibilidad de implementar un punto de distribución en vez de instalar otro sitio si se cumple alguna de las condiciones siguientes:**  

-   Su ancho de banda de red es suficiente para que equipos cliente de la ubicación remota se comuniquen con un punto de administración para descargar directivas de cliente y enviar información de inventario, de estado de generación de informes y de detección.  

-   El Servicio de transferencia inteligente en segundo plano (BITS) no proporciona un control de ancho de banda suficiente para sus requerimientos de red.  

 Para obtener más información sobre las opciones de administración de contenido de Configuration Manager, consulte [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Conceptos básicos de la administración de contenido en System Center Configuration Manager).  

##  <a name="bkmk_beyond"></a> Más allá de la topología de la jerarquía  
 Además de una topología de jerarquía inicial, considere qué servicios o funciones estarán disponibles en los diferentes sitios de la jerarquía (roles de sistema de sitio) y cómo se administrarán en la infraestructura las funciones y las configuraciones de la jerarquía. A continuación se muestran las consideraciones más comunes que se tratan en un tema independiente. Son importantes porque pueden influir en el diseño de jerarquía o puede verse afectadas por este:  

-   Durante la preparación para [administrar equipos y dispositivos con System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), considere si los dispositivos administrados residen de forma local, en la nube o incluyen dispositivos (BYOD) propiedad del usuario.  Además, considere cómo va a administrar los dispositivos que admiten varias opciones de administración, como los equipos con Windows 10 que se pueden administrar directamente mediante Configuration Manager o mediante la integración con Microsoft Intune.  

-   Conozca la manera en que la infraestructura de red disponible puede afectar al flujo de datos entre ubicaciones remotas (consulte [Prepare your network environment for System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains) (Preparar el entorno de red para System Center Configuration Manager)). Tenga en cuenta también dónde se ubican geográficamente los usuarios y los dispositivos administrados, y si tienen acceso o no a su infraestructura a través de su dominio corporativo o desde Internet.  

-   Planee una infraestructura de contenido para distribuir eficazmente la información que implemente (archivos y aplicaciones) en los dispositivos administrados (consulte [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Administración del contenido y de la infraestructura de contenido para System Center Configuration Manager)).  

-   Determine qué [características y funciones de System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) planea usar, los roles de sistema de sitio o la infraestructura de Windows que requieren y en qué sitios de una jerarquía de sitios múltiples puede implementarlos para conseguir el uso más eficaz de los recursos de la red y del servidor.  

-   Tenga en cuenta la seguridad de los datos y dispositivos, incluido el uso de una PKI. Vea [Requisitos de certificados PKI para System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Revise los siguientes recursos para configuraciones específicas de sitios:**  

-   [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Planear el proveedor de SMS de System Center Configuration Manager)  

-   [Plan for the site database for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md) (Planear la base de datos de sitio de System Center Configuration Manager)  

-   [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Planear servidores y roles de sistema de sitio para System Center Configuration Manager)  

-   [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md) (Planear la seguridad en System Center Configuration Manager)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) (Administrar el ancho de banda de red) cuando se implementa contenido dentro de un sitio  


**Tenga en cuenta las configuraciones que abarcan sitios y jerarquías:**  

-   [Opciones de alta disponibilidad para System Center Configuration Manager](/sccm/protect/understand/high-availability-options) para sitios y jerarquías

-   [Extender el esquema de Active Directory para System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) y configurar sitios para [publicar datos de sitio para System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Transferencias de datos entre sitios en System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Fundamentals of role-based administration for System Center Configuration Manager (Aspectos básicos de la administración basada en roles de System Center Configuration Manager)](../../../core/understand/fundamentals-of-role-based-administration.md)
