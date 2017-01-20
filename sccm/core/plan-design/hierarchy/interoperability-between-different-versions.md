---
title: Interoperabilidad entre versiones | System Center Configuration Manager
description: "Obtenga información sobre cómo evitar conflictos entre varias jerarquías de System Center Configuration Manager en la misma red."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: db0bf04b73050cb42f8230227c8db6ebfb3c6987


---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilidad entre diferentes versiones de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Es posible instalar y usar variar jerarquías independientes de System Center Configuration Manager en la misma red. En cambio, debido a que diferentes jerarquías de Configuration Manager no interoperan fuera de la migración, cada jerarquía requiere configuraciones para evitar conflictos entre ellas. Además, puede establecer algunas configuraciones para ayudar a los recursos que administra a interactuar con los sistemas del sitio desde la jerarquía correcta.  

 Las secciones siguientes proporcionan información acerca del uso de diferentes versiones de Configuration Manager en la misma red:  

-   [Interoperabilidad entre System Center Configuration Manager y versiones anteriores del producto](#BKMK_SupConfigInterop)  

-   [Interoperabilidad de la consola de Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitaciones de Configuration Manager en una jerarquía de versión mixta](#bkmk_mixed)  

##  <a name="a-namebkmksupconfiginteropa-interoperability-between-system-center-configuration-manager-and-earlier-product-versions"></a><a name="BKMK_SupConfigInterop"></a> Interoperabilidad entre System Center Configuration Manager y versiones anteriores del producto  
 Excepto durante el proceso de actualización de System Center 2012 Configuration Manager a System Center Configuration Manager o desde una versión de System Center Configuration Manager a una versión más reciente (mediante actualizaciones en la consola), los sitios de diferentes versiones no pueden coexistir en la misma jerarquía.  

 Dado que puede implementar un sitio y una jerarquía de System Center Configuration Manager en paralelo con un sitio o una jerarquía de System Center 2012 Configuration Manager existente, tome medidas para evitar que los clientes de una de las versiones intenten unirse a un sitio desde la otra. Por ejemplo, si dos o más jerarquías de Configuration Manager tienen límites que se superponen (consulte [Información sobre la superposición de límites](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md#BKMK_BoundaryOverlap)) que incluyen las mismas ubicaciones de red, se recomienda asignar cada nuevo cliente a un sitio específico en lugar de usar la asignación de sitio automática. Para obtener información sobre la asignación automática de sitios en System Center 2012 Configuration Manager, consulte [Cómo asignar clientes a un sitio en System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 Además, no se admite para instalar un cliente de System Center 2012 Configuration Manager en un equipo que hospede un rol de sistema de sitio de System Center Configuration Manager, ni para instalar un cliente de System Center Configuration Manager en un equipo que hospede un rol de sistema de sitio desde System Center 2012 Configuration Manager.  

 De manera similar, no se admiten los siguientes clientes ni la siguiente conexión de red privada virtual (VPN):  

-   Cualquier cliente de System Center 2012 Configuration Manager o una versión de cliente de equipo anterior  

-   Cualquier cliente de System Center 2012 Configuration Manager o un cliente de administración de dispositivos anterior  

-   Cliente de administración de dispositivos de Windows CE Platform Builder (cualquier versión)  

-   Conexión VPN de System Center Mobile Device Manager  

###  <a name="a-namebkmksupconfigsiteassignmenta-client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Consideraciones sobre la asignación de sitio de cliente  
 Los clientes de System Center Configuration Manager pueden asignarse solo a un único sitio primario. Cuando se usa la asignación automática de sitios para asignar clientes a un sitio durante la instalación del cliente, más de un grupo de límites incluye el mismo límite, y los grupos de límites tienen asignados diferentes sitios, no se podrá predecir la asignación de sitio real de un cliente.  

 Si los límites se superponen en varias jerarquías y varios sitios de Configuration Manager, es posible que los clientes no se asignen al sitio previsto o que no se asignen a ningún sitio.  

 Los clientes de System Center Configuration Manager comprueban la versión del sitio de Configuration Manager antes de completar la asignación de sitio y no pueden asignarse a una versión anterior si los límites del sitio se superponen. En cambio, los clientes de System Center 2012 Configuration Manager pueden asignarse de manera incorrecta a un sitio de System Center Configuration Manager.  

 Para evitar que los clientes se asignen de forma no intencionada al sitio incorrecto cuando dos jerarquías tienen límites que se superponen, configure los parámetros de instalación de cliente de Configuration Manager para asignar los clientes a un sitio específico.  

##  <a name="a-namebkmkmixeda-configuration-manager-limitations-in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> Limitaciones de Configuration Manager en una jerarquía de versión mixta  
 Durante el proceso de actualización de un sitio de System Center Configuration Manager, habrá ocasiones en que sitios diferentes tendrán distintas versiones.  Por ejemplo, puede actualizar un sitio de administración central a una nueva versión, pero debido a las ventanas de mantenimiento de sitio, uno o más sitios primarios podrían no actualizarse hasta una fecha y hora posterior.  

 Si varios sitios de una misma jerarquía ejecutan versiones diferentes, determinadas funciones no estarán disponibles. Esto puede afectar al modo en que administra objetos de Configuration Manager en la consola de Configuration Manager y a las funcionalidades disponibles para los clientes. Normalmente, la funcionalidad de la versión más actual de Service Pack de Configuration Manager no es accesible en sitios o para clientes que ejecutan una versión anterior del Service Pack.  

### <a name="limitations-when-upgrading-configuration-manager"></a>Limitaciones al actualizar Configuration Manager  

|Objeto|Detalles|  
|------------|-------------|  
|Cuenta de acceso a la red|**Si realiza la actualización de System Center 2012 Configuration Manager a System Center Configuration Manager:** si usa una consola de Configuration Manager conectada a un sitio de administración central actualizado a System Center Configuration Manager para ver los detalles de la cuenta de acceso a la red, la consola no mostrará los detalles de las cuentas que estén configuradas en un sitio primario que ejecute System Center 2012 Configuration Manager. Cuando el sitio primario se actualice a la misma versión que el sitio de administración central, los detalles de la cuenta serán visibles en la consola.<br /><br /> **Si realiza la actualización entre versiones de System Center Configuration Manager:** si usa una consola de Configuration Manager conectada a un sitio de administración central actualizado a una nueva versión de System Center Configuration Manager para ver los detalles de la cuenta de acceso a la red, la consola no mostrará los detalles de las cuentas que estén configuradas en un sitio primario que ejecute una versión anterior. Cuando el sitio primario se actualice a la misma versión que el sitio de administración central, los detalles de la cuenta serán visibles en la consola.|  
|Imágenes de arranque para la implementación de sistemas operativos|**Si realiza la actualización de System Center 2012 Configuration Manager a System Center Configuration Manager:** cuando el sitio de nivel superior de una jerarquía se actualiza a System Center Configuration Manager, las imágenes de arranque predeterminadas se actualizan automáticamente a imágenes de arranque basadas en Windows ADK 10. Use estas imágenes de arranque solo para implementaciones a clientes en sitios de System Center Configuration Manager. Para más información, consulte [Planeamiento de la interoperabilidad de la implementación de sistema operativo en System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Si realiza la actualización entre versiones de System Center Configuration Manager:** siempre y cuando las nuevas versiones de cm6long no actualicen la versión de Windows ADK en uso, no se producirá ningún efecto en las imágenes de arranque.|  
|Nuevas etapas de la secuencia de tareas|Cuando se crea una secuencia de tareas que contiene un paso de secuencia de tareas incluido en una versión de Configuration Manager que no está disponible en una versión anterior, pueden surgir los siguientes problemas:<br /><br /> -- Se produce un error al intentar editar la secuencia de tareas desde un sitio que ejecuta una versión anterior de Configuration Manager.<br /><br /> -- La secuencia de tareas no se ejecutará en un equipo que ejecuta una versión anterior del cliente de Configuration Manager.|  
|Comunicaciones entre cliente y punto de administración de nivel inferior|Un cliente de Configuration Manager que se comunica con un punto de administración desde un sitio que ejecuta una versión inferior solo puede usar la funcionalidad que la versión de nivel inferior de Configuration Manager admite. Por ejemplo, si implementa contenido de un sitio de System Center Configuration Manager que se actualizó recientemente a un cliente que se comunica con un punto de administración que aún no está actualizado a esa versión, ese cliente no podrá usar la funcionalidad nueva de la última versión.|  

##  <a name="a-namebkmkconsoleinteropa-interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Interoperabilidad de la consola de Configuration Manager  
 La tabla siguiente contiene información sobre el uso de la consola de Configuration Manager en un entorno con varias versiones de Configuration Manager.  

|Entorno de interoperabilidad|Más información|  
|----------------------------------|----------------------|  
|Un entorno con System Center 2012 Configuration Manager y System Center Configuration Manager|Para administrar un sitio de Configuration Manager, la consola y el sitio al que la consola se conecta deben ejecutar la misma versión de Configuration Manager. Por ejemplo, no puede usar una consola de System Center 2012 Configuration Manager para administrar un sitio de System Center Configuration Manager, o viceversa.<br /><br /> No se admite para instalar la consola de System Center 2012 Configuration Manager y la de System Center Configuration Manager en el mismo equipo.|  
|Un entorno con varias versiones de System Center Configuration Manager|System Center Configuration Manager no admite la instalación de más de una sola consola de Configuration Manager en un equipo. Para usar varias consolas de distintas versiones de System Center Configuration Manager, debe instalar las consolas en equipos independientes.<br /><br /> Durante el proceso de actualización de sitios en una jerarquía, puede conectar una consola a un sitio que ejecute una versión más reciente y visualizar la información de otros sitios de esa jerarquía. En cambio, esta configuración no se recomienda porque las diferencias entre la versión de la consola y la versión del sitio de Configuration Manager pueden dar lugar a problemas de datos y algunas características que están disponibles en la versión más reciente del producto no estarán disponibles en la consola.|  



<!--HONumber=Nov16_HO1-->


