---
title: "Aspectos básicos de sitios y jerarquías | Microsoft Docs"
description: "Obtenga información básica sobre los sitios y jerarquías de System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1b64b5f6e208b85a5ec2ef02bab34afee451c484
ms.openlocfilehash: cda27b9478e915bca99f5784ec6bcbedc989e841


---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Aspectos básicos de sitios y jerarquías para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Debe haber instalada una implementación de System Center Configuration Manager en un dominio de Active Directory y tener una base de uno o más sitios de Configuration Manager que formen una jerarquía. Desde un único sitio hasta una jerarquía de varios sitio, el tipo y la ubicación de los sitios que instale proporcionan la capacidad de escalar verticalmente (expandir) su implementación cuando sea necesario y ofrecer servicios clave a los usuarios y dispositivos administrados.

## <a name="hierarchies-of-sites"></a>Jerarquías de sitios
Al instalar System Center Configuration Manager por primera vez, el primer sitio de Configuration Manager que se instale determina el ámbito de la jerarquía: la base desde la que se administran los dispositivos y los usuarios de su empresa. Este primer sitio debe ser un sitio de administración central o un sitio primario independiente.  

 Un **sitio de administración central** es adecuado para implementaciones a gran escala y proporciona un punto central de administración y la flexibilidad necesaria para admitir dispositivos distribuidos por la infraestructura de red global. Después de instalar un sitio de administración central, tendrá que instalar uno o varios sitios primarios como sitios secundarios.  El motivo es que un sitio de administración central no admite directamente la administración de dispositivos, que es la función de un sitio primario. Un sitio de administración central admite varios sitios primarios secundarios que usará para administrar dispositivos y controlar el ancho de banda de red directamente cuando los dispositivos administrados estén en distintas ubicaciones geográficas.  

 Un **sitio primario independiente** es adecuado para implementaciones más pequeñas, y puede usarse para administrar dispositivos sin tener que instalar sitios adicionales. Mientras que un sitio primario independiente puede limitar el tamaño de la implementación, admite un escenario para expandir la jerarquía posteriormente mediante la instalación de un nuevo sitio de administración central. Con este escenario de expansión del sitio, su sitio primario independiente se convierte en un sitio primario secundario y, de este modo, podrá instalar sitios primarios secundarios adicionales por debajo de su nuevo sitio de administración central.  Gracias a ello, es posible ampliar la implementación inicial para el crecimiento futuro de su empresa.  

> [!TIP]  
>  En realidad, un sitio primario independiente y un sitio primario secundario son el mismo tipo de sitio: un sitio primario. La diferencia en el nombre se basa en la relación jerárquica que se crea cuando también se usa un sitio de administración central.  Esta relación jerárquica también puede limitar la instalación de determinados roles de sistema de sitio que amplían la funcionalidad de Configuration Manager. La razón es que determinados roles de sistema de sitio solo pueden instalarse en el sitio de nivel superior de la jerarquía, un sitio de administración central o un sitio primario independiente.  

 Después de instalar el primer sitio, puede instalar sitios adicionales.  Si el primer sitio era un sitio de administración central, puede instalar uno o varios sitios primarios secundarios.  Después de instalar un sitio primario (independiente o primario secundario), puede instalar uno o varios sitios secundarios.  

 Un **sitio secundario** solo puede instalarse como tal debajo de uno primario. Este tipo de sitio extiende el alcance de un sitio primario para administrar dispositivos en ubicaciones que tienen una conexión de red lenta con el sitio primario.   Aunque el sitio secundario extiende el sitio primario, los clientes se siguen administrando a través del sitio primario. El sitio secundario proporciona compatibilidad para los dispositivos en la ubicación remota mediante la compresión y la posterior administración de la transferencia de información a través de la red que envíe (implemente) a los clientes, y que los clientes envíen de nuevo a su sitio.  

 Los siguientes diagramas muestran algunos ejemplos de diseños de sitios.  

 ![Ejemplos de jerarquía](media/Hierarchy_examples.png)  

 Para obtener más información, consulte los temas siguientes:  

-   [Introducción a System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Diseñar una jerarquía de sitios para System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Instalar sitios de System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Servidores de sistema de sitio y roles de sistema de sitio  
 Cada sitio de Configuration Manager instala **roles del sistema de sitio** que admiten operaciones de administración.  Algunos roles se instalan de forma predeterminada cuando se instala un sitio, como el rol del **servidor de sitio** (que se asigna al equipo donde se instala el sitio) y el rol de servidor de base de datos de sitio (que se asigna al servidor SQL Server que hospeda la base de datos de sitio). Otros roles de sistema de sitio son opcionales y solo se utilizan cuando desea utilizar la funcionalidad que habilita un rol de sistema de sitio.  Cualquier equipo que hospede un rol de sistema de sitio se conoce como servidor de sistema de sitio.  

 Para una implementación más pequeña de Configuration Manager, es preferible que ejecute inicialmente todos los roles de sistema de sitio directamente en el equipo del servidor de sitio. Más adelante, a medida que crezcan el entorno administrado y las necesidades, se podrán instalar servidores de sistema de sitio adicionales para hospedar roles de sistema de sitio adicionales a fin de mejorar la eficiencia de los sitios en la provisión de servicios a más dispositivos.  

 Para obtener más información sobre los distintos roles de sistema de sitio, consulte [Roles de sistema de sitio](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) en [Planeamiento de servidores y roles de sistema de sitio para System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publicación de información de sitio en los Servicios de dominio de Active Directory  
 Para simplificar la administración de Configuration Manager, puede extender el esquema de Active Directory para admitir los detalles usados por Configuration Manager y, después, hacer que los sitios publiquen su información clave en Active Directory Domain Services (AD DS). Esto permite que los equipos que desea administrar recuperen de forma segura la información relacionada con el sitio de la fuente de confianza de AD DS. La información que los clientes pueden recuperar identifica los sitios disponibles, los servidores de sistema de sitio y los servicios que proporcionan dichos servidores.  

 **La extensión del esquema de Active Directory** se realiza solo una vez por bosque y puede hacerse antes o después de instalar Configuration Manager.   Al extender el esquema, debe crear un nuevo contenedor de Active Directory denominado **System Management** en cada dominio que contenga un sitio de Configuration Manager que publique datos que busquen los clientes. Para obtener más información, consulte [Extender el esquema de Active Directory para System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 **La publicación de datos del sitio** mejora la seguridad de su jerarquía de Configuration Manager y reduce la sobrecarga administrativa, pero no se necesita para la funcionalidad básica de Configuration Manager.  



<!--HONumber=Dec16_HO3-->


