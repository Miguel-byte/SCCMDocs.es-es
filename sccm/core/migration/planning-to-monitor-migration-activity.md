---
title: Supervisión de la migración
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar la consola de Configuration Manager para supervisar el progreso y la finalización correcta de los trabajos de migración.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2dfad7c9963862ff90934861973bf3862d745b98
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>Planear la supervisión de la actividad de migración en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Con System Center Configuration Manager, puede supervisar la migración en la consola de Configuration Manager, que se conecta a la jerarquía de destino. En la consola de Configuration Manager, situada en el área de trabajo **Administración**, puede usar el nodo **Migración** para supervisar el progreso y la finalización de los trabajos de migración. Puede ver información de resumen de cada trabajo de migración que identifica los objetos que se han migrado, los objetos que aún no se han migrado y el número de objetos excluidos de un trabajo de migración. También podrá ver detalles acerca de cualquier problema en la migración.  

## <a name="view-migration-progress"></a>Ver el progreso de la migración  
 Para ver el progreso de un trabajo de migración, use cualquiera de las siguientes acciones:  

-   En el área de trabajo **Administración** de la consola de Configuration Manager, expanda el nodo **Trabajos de migración**, seleccione un trabajo de migración y, después, seleccione la pestaña **Objetos en el trabajo**.  

-   Use los archivos de registro de Configuration Manager para revisar el progreso de la migración o para identificar problemas. El Administrador de migraciones es el proceso de Configuration Manager que efectúa un seguimiento de las acciones de migración y las registra en el archivo migmctrl.log en la carpeta **\&lt;InstallationPath\>\\LOGS** del servidor del sitio.  

    > [!NOTE]  
    >  Si se produce un error en un trabajo de migración, revise los detalles en el archivo migmctrl.log lo antes posible. Las entradas del registro de migración se agregan continuamente al archivo y sobrescriben los detalles antiguos. Si se sobrescriben las entradas, es posible que no pueda identificar si los problemas que puedan surgir con los objetos migrados se refieren a problemas de migración. La actividad de migración se registra en el sitio del nivel superior de la jerarquía, independientemente del sitio al que se conecta su consola de Configuration Manager cuando se configura la migración.  

-   Use los informes de Configuration Manager. Configuration Manager proporciona varios informes integrados de migración. También puede editar esos informes para que se ajusten a sus necesidades. Para obtener más información sobre los informes de Configuration Manager, consulte [Generación de informes en System Center Configuration Manager](../../core/servers/manage/reporting.md).  
