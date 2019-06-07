---
title: Interoperabilidad entre versiones
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo evitar conflictos entre varias jerarquías de Configuration Manager en la misma red.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51243f8df55f2736cfb053f9e38cc7b6716b2158
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354853"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidad entre diferentes versiones de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Puede instalar y usar varias jerarquías independientes de System Center Configuration Manager en la misma red. En cambio, debido a que diferentes jerarquías de Configuration Manager no interoperan fuera del proceso de migración, cada jerarquía requiere configuraciones para evitar conflictos entre ellas. Además, puede crear algunas configuraciones para ayudar a los recursos que administra a interactuar con los sistemas del sitio desde la jerarquía correcta.  

Las secciones siguientes proporcionan información acerca del uso de diferentes versiones de Configuration Manager en la misma red:  

- [Interoperabilidad entre System Center Configuration Manager y versiones anteriores del producto](#BKMK_SupConfigInterop)  

- [Interoperabilidad de la consola de Configuration Manager](#BKMK_ConsoleInterop)  

- [Limitaciones de Configuration Manager en una jerarquía de versión mixta](#bkmk_mixed)  


## <a name="BKMK_SupConfigInterop"></a> Interoperabilidad entre System Center Configuration Manager y versiones anteriores del producto  

Sitios de distintas versiones no pueden coexistir en la misma jerarquía de Configuration Manager. Las únicas excepciones son durante el proceso de los escenarios de actualización siguientes:

- Desde System Center 2012 Configuration Manager a System Center Configuration Manager.
- Desde una versión de System Center Configuration Manager a una versión más reciente con actualizaciones en la consola.

Puede implementar un sitio o jerarquía de System Center Configuration Manager en paralelo con un sitio o jerarquía de System Center 2012 Configuration Manager. Tome medidas para evitar que los clientes de alguna de las versiones intente unirse a un sitio desde la otra versión.

Por ejemplo, si dos o más jerarquías de Configuration Manager tienen [límites que se superponen](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries) que incluyen las mismas ubicaciones de red, asigne cada nuevo cliente a un sitio específico en lugar de usar la asignación de sitio automática. Para obtener más información, vea [Cómo asignar clientes a un sitio](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Además, no se puede instalar un cliente desde System Center 2012 Configuration Manager en un equipo que hospeda un rol de sistema de sitio desde System Center Configuration Manager. Tampoco puede instalar un cliente de System Center Configuration Manager en un equipo que hospeda un rol de sistema de sitio desde System Center 2012 Configuration Manager.  

No se admiten los clientes y las conexiones siguientes:  

- Cualquier cliente de System Center 2012 Configuration Manager o una versión de cliente de equipo anterior  

- Cualquier cliente de System Center 2012 Configuration Manager o un cliente de administración de dispositivos anterior  

- Cliente de administración de dispositivos de Windows CE Platform Builder (cualquier versión)  

- Conexión VPN de System Center Mobile Device Manager  

### <a name="BKMK_SupConfigSiteAssignment"></a> Consideraciones sobre la asignación de sitio de cliente  

Los clientes de Configuration Manager pueden asignarse solo a un único sitio primario. No es posible predecir la asignación de sitio real de un cliente cuando se cumplen todas las condiciones siguientes:

- Se usa la asignación de sitio automática para asignar clientes a un sitio durante la instalación de cliente.
- Más de un grupo de límites incluye el mismo límite.
- Los grupos de límites tienen distintos sitios asignados.

Si los límites se superponen en varias jerarquías y varios sitios de ConfigurationYou use automatic site assignment to assign clients to a site during client installationManager, es posible que los clientes no se asignen al sitio previsto o que no se asignen a ningún sitio.  

Los clientes de System Center Configuration Manager comprueban la versión del sitio antes de completar la asignación de sitio. Si los límites de sitio se superponen, no puede asignar clientes a un sitio con una versión anterior. Sin embargo, los clientes de System Center 2012 Configuration Manager anteriores podrían asignarse de manera incorrecta a un sitio de System Center Configuration Manager posterior.  

Para evitar que los clientes se asignen de forma no intencionada al sitio incorrecto cuando dos jerarquías tienen límites que se superponen, configure los parámetros de instalación de cliente para asignar los clientes a un sitio específico.  

## <a name="bkmk_mixed"></a> Limitaciones de Configuration Manager en una jerarquía de versión mixta  

Cuando actualiza una jerarquía de System Center Configuration Manager, habrá ocasiones en que sitios distintos tendrán distintas versiones. Por ejemplo, en primer lugar se actualiza el sitio de administración central. Debido a las ventanas de mantenimiento del sitio, no actualiza los sitios principales hasta una hora y fecha posteriores.  

Si varios sitios de una misma jerarquía ejecutan versiones diferentes, determinadas funcionalidades no estarán disponibles. Este comportamiento puede afectar al modo en que se administran los objetos de Configuration Manager en la consola de Configuration Manager y a las funcionalidades disponibles para los clientes. Normalmente, la funcionalidad de la versión más actual de Configuration Manager no es accesible en sitios o para clientes que ejecutan una versión anterior del Service Pack.  

### <a name="network-access-account"></a>Cuenta de acceso a la red

Actualiza el sitio de administración central a System Center Configuration Manager. Ve los detalles de la cuenta de acceso de red desde una consola de Configuration Manager que está conectada a este sitio actualizado. No muestra los detalles de la cuenta desde sitios que todavía ejecutan System Center 2012 Configuration Manager.

Después de actualizar el sitio principal a la misma versión que el sitio de administración central, los detalles de la cuenta serán visibles en la consola.

El mismo comportamiento se aplica cuando se actualiza entre versiones de System Center Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Imágenes de arranque para la implementación del sistema operativo

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-system-center-configuration-manager"></a>Si realiza la actualización de System Center 2012 Configuration Manager a System Center Configuration Manager

Cuando el sitio de nivel superior de una jerarquía se actualiza a System Center Configuration Manager, actualiza automáticamente las imágenes de arranque predeterminadas para usar la versión 10 de Windows Assessment and Deployment Kit (ADK). Use estas imágenes de arranque solo para implementaciones a clientes en sitios de System Center Configuration Manager. Para obtener más información, vea [Planeamiento de la interoperabilidad de la implementación de sistema operativo](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).

#### <a name="when-upgrading-between-system-center-configuration-manager-versions"></a>Si realiza la actualización entre versiones de System Center Configuration Manager

siempre y cuando las nuevas versiones de Configuration Manager no actualicen la versión de Windows ADK en uso, no se producirá ningún efecto en las imágenes de arranque.

### <a name="new-task-sequence-steps"></a>Nuevas etapas de la secuencia de tareas

Cuando se crea una secuencia de tareas con un paso incluido en una versión de Configuration Manager que no está disponible en una versión anterior, pueden surgir los siguientes problemas:

- Se produce un error al intentar editar la secuencia de tareas desde un sitio que ejecuta una versión anterior de Configuration Manager.

- La secuencia de tareas no se ejecutará en un equipo que ejecuta una versión anterior del cliente de Configuration Manager.

### <a name="client-to-down-level-management-point-communications"></a>Comunicaciones entre cliente y punto de administración de nivel inferior

Un cliente de Configuration Manager que se comunica con un punto de administración desde un sitio que ejecuta una versión inferior solo puede usar la funcionalidad que la versión de nivel inferior de Configuration Manager admite. Por ejemplo, si implementa contenido de un sitio de System Center Configuration Manager que se ha actualizado recientemente a un cliente que se comunica con un punto de administración que aún no está actualizado a esa versión, ese cliente no podrá usar la funcionalidad nueva de la última versión.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Implementaciones de secuencia de tareas y paquetes a clientes heredados

<!-- SCCMDocs-pr issue #3493 -->

A partir de la versión 1902, no se puede implementar un paquete o una secuencia de tareas en una versión de cliente 5.7730 o anterior. Para solucionar esta limitación, actualice el cliente a una versión posterior.


## <a name="BKMK_ConsoleInterop"></a> Interoperabilidad de la consola de Configuration Manager  

Esta sección contiene información sobre el uso de la consola de Configuration Manager en un entorno con varias versiones de Configuration Manager.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-system-center-configuration-manager"></a>Un entorno con System Center 2012 Configuration Manager y System Center Configuration Manager

Para administrar un sitio de Configuration Manager, la consola y el sitio al que la consola se conecta deben ejecutar la misma versión de Configuration Manager. Por ejemplo, no puede usar una consola de System Center 2012 Configuration Manager para administrar un sitio de System Center Configuration Manager ni viceversa.

No se permite instalar la consola de System Center 2012 Configuration Manager y la de System Center Configuration Manager en el mismo equipo.

### <a name="an-environment-with-multiple-versions-of-system-center-configuration-manager"></a>Un entorno con varias versiones de System Center Configuration Manager

System Center Configuration Manager no admite la instalación de más de una consola de Configuration Manager en un equipo. Para usar varias consolas de distintas versiones de System Center Configuration Manager, instale las consolas en equipos independientes.

Durante el proceso de actualización a una nueva versión de los sitios de una jerarquía, puede conectar una consola a un sitio que ejecute una versión más reciente y visualizar la información de otros sitios de esa jerarquía. Aun así, no se recomienda esta configuración. Es posible que las diferencias entre la versión de la consola y la versión del sitio de Configuration Manager pueden dar lugar a problemas en los datos. Además, algunas características que están disponibles en la versión más reciente del producto no estarán disponibles en la consola.

No se puede administrar un sitio con una consola de una versión que no coincida con la del sitio. Hacerlo podría provocar la pérdida de los datos y poner su sitio en riesgo. Por ejemplo, no se permite usar una consola de la versión 1610 para administrar un sitio que ejecute la versión 1606.
