---
title: "Escenarios de instalación | System Center Configuration Manager"
description: "Aprenda técnicas para instalar una nueva jerarquía de Configuration Manager mientras efectúa una actualización."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 90a802cbdfd6d0acd60ec462ffbf2a08c012eaeb


---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Escenarios para simplificar la instalación de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Con el lanzamiento de las versiones de actualización de la rama actual de System Center Configuration Manager, existen nuevos escenarios que simplifican la instalación de una nueva jerarquía en una versión de actualización (como la actualización 1602) y para actualizar desde Microsoft System Center 2012 Configuration Manager.  

Entre los escenarios admitidos se incluyen:  

**Instalación de una nueva jerarquía de la rama actual de System Center Configuration Manager** que ejecuta una versión actualizada:  

-   Instale solo el sitio de nivel superior seguido inmediatamente de la instalación de una actualización para mostrar el sitio con la versión de actualización que usará. Luego, puede instalar sitios adicionales directamente en esa versión de actualización.  

-   Este escenario omite la instalación de sitios adicionales en un nivel de línea base y luego tener que actualizarlos a la versión de actualización que quiera usar.  

-   Este escenario omite la instalación de clientes en una versión de línea de base y luego tener que instalarlos de nuevo cuando actualice a una versión posterior.  

**Actualización de la infraestructura de Microsoft System Center 2012 Configuration Manager** a una versión de actualización de System Center Configuration Manager:  

-   Actualice manualmente el sitio de administración central y cada sitio primario a una versión de línea de base (como 1511) antes de instalar una versión de actualización (como 1602).  

-   No actualice sitios secundarios desde Microsoft System Center 2012 Configuration Manager hasta que los sitios primarios ejecuten la versión de actualización que se va a usar.  

-   No actualice clientes desde Microsoft System Center 2012 Configuration Manager hasta que los sitios primarios ejecuten la versión de actualización que se va a usar.  

## <a name="scenario---install-a-new-hierarchy-to-an-update-version"></a>Escenario: Instalación de una nueva jerarquía en una versión de actualización  
En este escenario de ejemplo, se instala el primer sitio de una jerarquía mediante una versión de línea de base de System Center Configuration Manager, versión 1511. Luego, instala la actualización 1602 antes de implementar sitios o clientes adicionales.  

-   Como tiene pensado usar una versión de actualización (como 1602) y no permanecer en una versión de línea de base (como 1511), no es necesario instalar sitios adicionales y luego actualizarlos, o instalar y luego actualizar los clientes.  

-   No instala sitios secundarios con la versión 1511 y luego los actualiza a 1602. Lo que hace es instalarlos después de que los sitios primarios ejecuten 1602.  

**Utilice la siguiente secuencia:**  

1.  **Instale un sitio de nivel superior para su nueva jerarquía** usando los medios de línea de base.  

    -   Solo puede utilizar medios de línea de base para instalar el primer sitio de una nueva jerarquía.  

    -   Por ejemplo, instale un sitio de nivel superior con la versión de línea de base de 1511. Consulte [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites) (Uso del asistente para la instalación para instalar sitios).  

    Después de este paso, el sitio de nivel superior ejecuta la versión 1511.  

2.  **Use actualizaciones integradas en la consola para actualizar el sitio de nivel superior a una versión posterior.**  

    -   Antes de instalar los clientes o los sitios secundarios, actualice el sitio de nivel superior a la versión de actualización que tiene pensado usar.  

    -   Por ejemplo, puede actualizar el sitio de nivel superior que ejecuta la versión 1511 a la versión 1602. Consulte [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md) (Actualizaciones para System Center Configuration Manager).  

    Después de este paso, el sitio de nivel superior ejecuta la versión 1602.  

3.  **Instale nuevos sitios primarios secundarios debajo de un sitio de administración central.**  

    -   Utilice los medios de instalación de la carpeta CD.Latest en el servidor de sitio de administración central para instalar sitios primarios secundarios.  Consulte [The CD.Latest folder for System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md) (La carpeta CD.Latest para System Center Configuration Manager).  

        -   Estos medios de origen son necesarios para garantizar que los nuevos sitios secundarios coinciden con la versión del sitio de administración central.  

    Después de este paso, los nuevos sitios primarios secundarios ejecutan la versión 1602.  

4.  **En cada sitio primario, utilice la opción integrada en la consola para instalar nuevos sitios secundarios.**  

    -   Como no ha instalado sitios secundarios mientras los sitios primarios estaban en la versión 1511, no será necesario actualizar los sitios secundarios.  

    -   En su lugar, instale nuevos sitios secundarios que ejecuten la versión 1602. Consulte *Install a secondary site* (Instalar un sitio secundario) en [Use the Setup Wizard to install sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites) (Uso del asistente para la instalación para instalar sitios).  

    Después de este paso, se instalan nuevos sitios secundarios que ejecutan la versión 1602.  

5.  **Instale nuevos clientes en el sitio primario.**  

    -   Como no ha instalado clientes mientras los sitios primarios estaban en la versión 1511, no será necesario actualizar los clientes de la versión 1511 a la versión 1602.  

    -   En su lugar, instale nuevos clientes que ejecuten la versión 1602. Consulte [Deploy clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md) (Implementar clientes en System Center Configuration Manager).  

    Después de este paso, se instalan nuevos clientes que ejecutan la versión 1602.  

## <a name="scenario---upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Escenario: Actualización de System Center 2012 Configuration Manager a una versión de actualización de la rama actual de System Center Configuration Manager  
En este escenario de ejemplo actualizará la infraestructura de Microsoft System Center 2012 Configuration Manager a una versión de actualización de System Center Configuration Manager, como la versión 1602.  

-   El sitio de administración central y cada sitio primarios se deben actualizar a la versión de línea de base 1511 antes de instalar la actualización de la versión 1602.  

-   Los clientes y los sitios secundarios no instalan la versión 1511 ni se actualizan a ella. En su lugar, pasan directamente de Microsoft System Center 2012 Configuration Manager a la versión 1602 de System Center Configuration Manager.  

**Utilice la siguiente secuencia:**  

1.  **Actualice el sitio de nivel superior de Microsoft System Center 2012 Configuration Manager** a una versión de línea de base de la rama actual usando los medios de origen de System Center Configuration Manager (por ejemplo, la versión 1511). Consulte [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).  

    -   Al igual que los escenarios de actualización tradicionales, actualice siempre primero el sitio de nivel superior de la jerarquía y luego los sitios secundarios.  

    Después de este paso, el sitio de nivel superior ejecuta 1511.  

2.  **Actualice cada sitio primario secundario de la jerarquía** a esa misma versión de línea de base.  

    -   Si actualiza desde Microsoft System Center 2012 Configuration Manager, debe actualizar manualmente cada sitio primario a una versión de línea de base de la rama actual.  

    -   En este momento, no actualizará los sitios secundarios.  

    Después de este paso, cada sitio primario ejecuta la versión 1511.  

3.  **Establezca las ventanas de mantenimiento en los sitios primarios secundarios.** Después de actualizar todos los sitios primarios a la versión de línea de base, tiene pensado configurar ventanas de mantenimiento para controlar cuándo esos sitios instalarán actualizaciones de la infraestructura. Consulte [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md) (Cómo usar las ventanas de mantenimiento en System Center Configuration Manager).  (Las ventanas de mantenimiento se conocen como ventanas de servicio en la versión 1511.)  

    -   Un sitio primario secundario instala automáticamente las mismas actualizaciones que se instalan en un sitio de administración central.  

    -   Los sitios secundarios no instalan automáticamente nuevas versiones y se deben actualizar manualmente desde la consola.  

    > [!NOTE]  
    >  Si usa la versión 1511 y quiere usar ventanas de mantenimiento, primero debe instalar la revisión del [artículo 3142341 de Microsoft Knowledge Base](http://support.microsoft.com/kb/3142341). Este problema se resuelve al instalar la actualización 1602.  

    Después de este paso, al instalar actualizaciones en el sitio de administración central, los sitios primarios secundarios solo instalarán esa actualización cuando así se lo permita la ventana de mantenimiento.  

4.  **Instale la versión de actualización en el sitio de nivel superior.** De esta forma se actualiza el sitio de nivel superior. Después de que un sitio de administración central instala la versión de actualización, cada sitio primario secundario instala automáticamente la actualización a menos que una ventana de mantenimiento la bloquee.  

    -   Por ejemplo, puede actualizar el sitio de nivel superior de la versión 1511 a la versión 1602. Consulte [Updates for System Center Configuration Manager](../../../../core/servers/manage/updates.md) (Actualizaciones para System Center Configuration Manager).  

    Después de este paso, el sitio de administración central y cada sitio primarios ejecutan la versión 1602.  

5.  **Actualice los sitios secundarios.** Después de que un sitio primario instala la actualización y ejecuta la versión 1602, utilice la opción integrada en la consola para actualizar los sitios secundarios.  

    -   De esta forma, se actualizan los sitios secundarios directamente desde Microsoft System Center 2012 Configuration Manager a la versión de actualización instalada en el sitio primario.  

    -   Para obtener información sobre cómo actualizar un sitio secundario, consulte [Upgrade sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) (Actualizar sitios) en [Upgrade to System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Actualizar a System Center Configuration Manager).  

6.  **Actualice los clientes.** Aplique la información que se describe en [How to upgrade clients for Windows computers in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) (Actualizar clientes de equipos Windows con System Center Configuration Manager).  

    -   De esta forma, se actualizan los clientes directamente desde Microsoft System Center 2012 Configuration Manager a la versión de actualización instalada en el sitio primario.  

    Después de este paso, los clientes se actualizan a la versión 1602 sin actualizarse primero a la versión 1511.



<!--HONumber=Nov16_HO1-->


