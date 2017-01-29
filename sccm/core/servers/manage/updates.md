---
title: Actualizaciones | Microsoft Docs
description: "Obtenga información sobre un método de servicio en la consola denominado **Actualizaciones y mantenimiento** que facilita la ubicación e instalación de las actualizaciones recomendadas."
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
caps.latest.revision: 51
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5314bcb434b5b540f80cdfe32002df7b8fed6195
ms.openlocfilehash: 52d5ad7a348e0489f43ac6cb46af930499ef6cf2


---
# <a name="updates-for-system-center-configuration-manager"></a>Actualizaciones para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

System Center Configuration Manager usa un método de servicio en la consola denominado **Actualizaciones y mantenimiento** que facilita la búsqueda e instalación de las actualizaciones recomendadas para la infraestructura de Configuration Manager. Este método de servicio en la consola se complementa con actualizaciones fuera de banda, como revisiones destinadas a los clientes que necesitan solucionar problemas que pueden ser específicos para su entorno.  

> [!TIP]
> Al administrar el sitio de System Center Configuration Manager y la infraestructura de la jerarquía, los términos *actualizar* ** e *instalar* se usan para describir tres conceptos independientes. Para obtener información sobre cómo se usa cada término, vea [Acerca de la actualización e instalación](/sccm/core/understand/upgrade-update-install).


 **Los temas siguientes pueden ayudarle a obtener información sobre cómo encontrar e instalar los distintos tipos de actualizaciones para System Center Configuration Manager:**  

-   [Instalación de actualizaciones en la consola para System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  

-   [Uso de la herramienta de conexión de servicio para System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md)  

-   [Uso de la herramienta de registro de actualizaciones para importar revisiones en System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md)  

-   [Uso del instalador de revisiones para instalar actualizaciones para System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  


Si usa la rama de Technical Preview, consulte [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) (Technical Preview para System Center Configuration Manager) para obtener información adicional específica de esa rama.


##  <a name="a-namebkmkbaselinesa-baseline-and-update-versions"></a><a name="bkmk_Baselines"></a> Versiones de línea de base y versiones de actualización  
 La versión inicial de la rama actual de System Center Configuration Manager era la versión 1511, que es una versión de línea base. La versión 1606 se ha publicado como una línea base posteriormente:  

-   Use la versión de línea de base más reciente cuando instale un sitio nuevo en una jerarquía nueva.  

-   Debe usar una versión de línea de base para actualizar desde System Center 2012 Configuration Manager.  

-   Las versiones de línea base adicionales se publicarán periódicamente. Al usar la última versión de línea base para instalar una nueva jerarquía, evita tener que instalar una versión obsoleta de Configuration Manager y luego una actualización de su infraestructura para actualizarla.  

Una vez que instala una versión de línea de base, las versiones adicionales de Configuration Manager se encuentran disponibles como actualizaciones en la consola. Las actualizaciones en la consola actualizan la infraestructura a la versión más reciente de Configuration Manager.  

-   Las actualizaciones en la consola se instalan para actualizar la versión del sitio de primer nivel.  

-   Las actualizaciones que instala en el sitio de administración central se instalarán automáticamente en los sitios principales secundarios, a menos que los bloquee una ventana de mantenimiento que se haya configurado en el sitio principal.  

-   Debe actualizar manualmente los sitios secundarios a una versión de actualización nueva desde la consola.  

Cuando instala una actualización, esta almacena los archivos de instalación de esa versión en el servidor de sitio, en una carpeta llamada CD.Latest. Consulte [La carpeta CD.Latest para System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md) para obtener más información sobre estos archivos.  

-   Use los archivos de la carpeta CD.Latest durante la recuperación del sitio y para instalar sitios adicionales en una jerarquía que ya no ejecuta una versión de línea de base.  

-   No puede usar archivos de instalación desde la carpeta CD.Latest para instalar el primer sitio de una jerarquía nueva o para actualizar un sitio desde System Center 2012 Configuration Manager.  

Algunas actualizaciones de Configuration Manager se encuentran disponibles tanto como una versión de actualización en la consola para la infraestructura existente como una versión de línea de base nueva.  

Las siguientes versiones de Configuration Manager están disponibles como línea de base, actualización, o ambas:  

|Versión|Fecha de disponibilidad|Línea de base|Actualización en la consola|  
|-------------|-----------------------|--------------|------------------------|  
|**1511**<br /><br /> 5.00.8325.1000|12/8/2015|Sí|No|  
|**1602**<br /><br /> 5.00.8355.1000|3/11/2016|No|Sí|
|**1606**<br /><br /> 5.00.8412.1000|22/7/2016|No|Sí|
|**1606** con el paquete acumulativo de revisiones 1606 (KB3186654) </br></br>5.00.8412.1307 *(Nota 1)* |12/10/2016|Sí|No|
|**1610**<br /><br /> 5.00.8458.1000|18/11/2016|No|Sí|
*(Nota 1)* Este medio de línea base 1606 está disponible como parte de Microsoft System Center 2016 o de una versión de System Center Configuration Manager (rama actual y rama de mantenimiento a largo plazo 1606).

Para comprobar la versión del sitio de Configuration Manager, vaya a **Acerca de System Center Configuration Manager** en la esquina superior izquierda de la consola, donde aparece la nueva versión del sitio y la consola.  

##  <a name="a-namebkmkinconsolea-in-console-updates-and-servicing"></a><a name="bkmk_inconsole"></a> Actualizaciones y servicio en la consola  
 Cuando usa una instalación lista para producción de System Center Configuration Manager, a la que también se conoce como rama actual, la mayoría de las actualizaciones que se instalan están disponibles con el canal Actualizaciones y mantenimiento. Este método identifica, descarga y pone a disposición las actualizaciones que se aplican a la versión y la configuración actual de la infraestructura e incluye solo las actualizaciones que Microsoft recomienda para todos los clientes.   
 Entre ellos, se incluye:  

-   Versiones nuevas, como la versión 1602.  

-   Actualizaciones, que incluyen características nuevas para la versión actual.  

-   Revisiones para la versión de Configuration Manager y que todos los clientes deberían instalar.  

Las actualizaciones en la consola proporcionan mayor estabilidad y solucionan problemas comunes. Estas actualizaciones reemplazan los tipos de actualización vistos para versiones anteriores del producto por Service Packs, actualizaciones acumulativas, revisiones aplicables a todos los clientes y la extensión para Microsoft Intune. Estas actualizaciones se pueden aplicar a una o varias de las siguientes opciones:  

-   Servidores de sitio principal y de administración central  

-   Roles de sistema de sitio y servidores de sistema de sitio  

-   Instancias del proveedor de SMS  

-   Consolas de Configuration Manager  

-   Clientes de Configuration Manager  

Configuration Manager detecta las actualizaciones nuevas que tiene disponibles cuando se sincroniza el rol de sistema de sitio del punto de conexión de servicio con el servicio en la nube y el Centro de descarga de Microsoft:  

-   Cuando el punto de conexión de servicio está en modo en línea, el sitio se sincroniza con Microsoft cada día para identificar automáticamente las actualizaciones nuevas que se aplican a la infraestructura.  Para descargar las actualizaciones y los archivos de redistribución de actualizaciones, el equipo que hospeda el rol de sistema de sitio del punto de conexión de servicio usa el contexto **System** para obtener acceso a las siguientes ubicaciones de Internet: go.microsoft.com y download.microsoft.com. Para obtener información sobre las ubicaciones adicionales a las que se conecta el punto de conexión de servicio, consulte [Requisitos de acceso a Internet](../../../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_urls) en [Acerca del punto de conexión de servicio en System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Cuando el punto de conexión de servicio está en modo sin conexión, se usa la herramienta de conexión de servicio para realizar manualmente la sincronización con la nube de Microsoft. Para obtener más información, consulte [Uso de la herramienta de conexión de servicio para System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

-   Las actualizaciones en la consola reemplazan la necesidad de ubicar e instalar de manera independiente las actualizaciones individuales, Service Packs y características nuevas.  

-   Solo instala las actualizaciones en la consola de su preferencia y, cuando instale algunas actualizaciones, podrá seleccionar las características individuales que desea habilitar y usar. Para obtener más información, consulte [Habilitar características opcionales de las actualizaciones](../../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Cuando se instala una actualización en la consola:  

-   Ejecuta automáticamente una comprobación de los requisitos previos. También puede ejecutar esta comprobación antes de comenzar la instalación.  

-   Se instala en el sitio de administración central (si lo tiene) y en los sitios principales, de manera automática. Puede controlar cuándo cada servidor de sitio primario tiene permitido actualizar su infraestructura con [Ventanas de servicio para servidores de sitio](../../../core/servers/manage/service-windows.md).  

-   Una vez que un servidor de sitio se actualiza, se actualizan automáticamente todos los roles de sistema de sitio afectados (incluidas las instancias del proveedor de SMS). Las consolas de Configuration Manager también le piden al usuario de la consola que la actualice una vez que el sitio instala la actualización.  

-   Si una actualización incluye el cliente de Configuration Manager, tiene la opción de probar la actualización en el entorno de preproducción o de aplicar la actualización de forma inmediata a todos los clientes.  

-   Una vez que se actualiza un sitio principal, los sitios secundarios no se actualizan automáticamente. En lugar de eso, es usted quien debe iniciar la actualización de los sitios secundarios.  

> [!NOTE]  
>  La versión de producción de System Center Configuration Manager (rama actual), la rama de mantenimiento a largo plazo y Technical Preview para System Center Configuration Manager son diferentes versiones. Por lo tanto, las actualizaciones que se aplican para una rama no están disponibles como actualizaciones en la consola para las demás ramas. Para más información sobre las diferentes ramas, consulte [Which branch of Configuration Manager should I use (¿Qué rama de Configuration Manager debo usar?)](/sccm/core/understand/which-branch-should-i-use).

##  <a name="a-namebkmkoutofbanda-out-of-band-hotfixes"></a><a name="bkmk_outofband"></a> Revisiones fuera de banda  
Algunas revisiones se lanzan con disponibilidad limitada para abordar problemas específicos, o bien son aplicables para todos los clientes, pero no se pueden instalar con el método en la consola. Estas revisiones se entregan fuera de banda y no se detectan desde el servicio en la nube de Microsoft.  

Habitualmente, obtiene información sobre las revisiones fuera de banda desde los servicios de asistencia al cliente de Microsoft, un artículo de Knowledge Base o desde el [blog del equipo de System Center Configuration Manager](https://blogs.technet.microsoft.com/configmgrteam) cuando busca corregir o enfrentar un problema con la implementación de Configuration Manager.  

Estas revisiones se instalan manualmente, mediante uno de estos dos métodos:  

-   **Herramienta de registro de actualizaciones:** esta herramienta importa de forma manual la revisión a la consola de Configuration Manager donde luego puede instalar la actualización como lo haría con las actualizaciones en la consola que se detectan de forma automática. Este método se usa para las actualizaciones que usan la siguiente estructura de nombre de archivo: **.update.exe**.  El nombre de archivo completo de este tipo de revisión es similar al siguiente: **&lt;Producto\>-&lt;versión del producto\>-&lt;identificador del artículo de KB\>-ConfigMgr.Update.exe**.  

     Para obtener más información, consulte [Use the Update Registration Tool to import hotfixes to System Center Configuration Manager](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md) (Uso de la herramienta de registro de actualizaciones para importar revisiones en System Center Configuration Manager).  

-   **Instalador de revisiones:** esta herramienta se usa para instalar manualmente una revisión que no se puede instalar con el método en la consola. Este método se usa para las revisiones que usan la siguiente estructura de nombre de archivo: **&lt;Producto\>-&lt;versión del producto\>-&lt;identificador del artículo de KB\>-&lt;plataforma\>-&lt;idioma\>.exe**.

     Para obtener más información, consulte [Use the Hotfix Installer to install updates for System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md) (Uso del instalador de revisiones para instalar actualizaciones para System Center Configuration Manager).



<!--HONumber=Jan17_HO2-->


