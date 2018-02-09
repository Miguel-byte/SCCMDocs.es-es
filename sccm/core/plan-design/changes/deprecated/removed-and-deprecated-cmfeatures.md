---
title: "En desuso para características de Configuration Manager"
titleSuffix: Configuration Manager
description: "Obtenga información sobre las características que System Center Configuration Manager ya no admite."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Características eliminadas y en desuso de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este artículo se describen las características que dejaron de ser compatibles con System Center Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). En este artículo se proporciona información anticipada sobre los cambios futuros que puedan afectar a su uso de Configuration Manager.  

Esta información está sujeta a cambios en versiones futuras y puede no incluir todas las características en desuso de Configuration Manager.

## <a name="deprecated-features"></a>Características en desuso  

|**Característica**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Con la llegada de la nueva experiencia del Centro de software con la versión 1511, las aplicaciones que solo se hubiesen mostrado en el catálogo de aplicaciones (aplicaciones disponibles para el usuario) ahora aparecen en el Centro de software. </br></br>Con esta funcionalidad principal del catálogo de aplicaciones incluida ahora en el Centro de software, la experiencia del catálogo de aplicaciones basada en la Web dejará de estar disponible en los próximos meses.|11 de agosto de 2017| La compatibilidad con la experiencia del usuario con el sitio web del catálogo de aplicaciones finaliza con la primera actualización publicada después del 1 de junio de 2018.|
|El Centro de software tiene un aspecto renovado y moderno. En los próximos meses, la versión anterior del Centro de software dejará de estar disponible.<br><br>Puede configurar los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Agente de equipo** > **Use new Software Center** (Usar el nuevo Centro de software).<br><br>Para más información sobre el Centro de software, consulte [Planear y configurar la administración de aplicaciones en System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de diciembre de 2016|La compatibilidad con la versión anterior del Centro de software finaliza con la primera actualización publicada después del 1 de enero de 2018.|
|Administración de discos duros virtuales (VHD) con Configuration Manager. </br></br>Esto incluye la eliminación de opciones para crear un nuevo VHD o administrar un VHD con una secuencia de tareas, y la eliminación del nodo de discos duros virtuales de la consola de Configuration Manager. </br></br>Cuando se quita esta compatibilidad, los VHD existentes no se eliminarán, pero ya no se podrá obtener acceso a ellos desde dentro de la consola de Configuration Manager.  |6 de enero de 2017 |Versión 1710|
|Secuencias de tareas: <br /> - Convertir el disco en dinámico <br /> - Instalar herramientas de implementación |18 de noviembre de 2016|Versión 1710|
|Herramienta de evaluación de actualizaciones de System Center Configuration Manager. </br></br>La Herramienta de evaluación de actualizaciones depende de System Center Configuration Manager y del kit de herramientas de compatibilidad de aplicaciones (ACT) 6.x. La versión final de ACT se ha entregado en Windows 10 v1511 ADK. Como no habrá más actualizaciones para ACT, se interrumpirá el soporte para la Herramienta de evaluación de actualizaciones. </br></br>La Herramienta de evaluación de actualizaciones se reemplaza por la característica [Preparación de actualización](/sccm/core/clients/manage/upgrade/upgrade-analytics). El aviso de desuso se agregó a la [página de descarga de UAT](https://www.microsoft.com/download/details.aspx?id=37145) el 12 de septiembre de 2016. | 12 de septiembre de 2016  | 11 de julio de 2017 |
|Secuencias de tareas: <br /> - OSDPreserveDriveLetter  <br /><br /> Ahora, durante una implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:). Si quiere especificar otra unidad, puede cambiar la ubicación en el paso de secuencia de tareas Aplicar el sistema operativo. Vaya a la opción de configuración **Seleccionar la ubicación en la que desea aplicar este sistema operativo**. Seleccione **Letra de unidad lógica específica** y elija la unidad que desee utilizar. |20 de junio de 2016 |Versión 1606 |
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|10 de julio de 2015|Versión 1511|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|16 de octubre de 2015|Versión 1511|



<br></br>
Detalles adicionales sobre las características eliminadas con la versión 1511 de System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Administración fuera de banda  
 Con Configuration Manager, se ha quitado la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager.  

-   Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). El complemento permite el acceso a las funciones más recientes para administrar AMT, a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

-   La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio.  

###  <a name="bkmk_nap"></a> Protección de acceso a redes  
 System Center Configuration Manager ha eliminado la compatibilidad con Protección de acceso a redes. La característica quedó en desuso en Windows Server 2012 R2 y se eliminó en Windows 10.  

 Para alternativas de protección de acceso a redes, consulte la sección *Funcionalidad en desuso* de [Información general sobre servicios de acceso y directivas de redes](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="more-information"></a>Más información
Para obtener más información, vea:
 - [Elementos eliminados y en desuso](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Sitio web de la [directiva de ciclos de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).
 - [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
