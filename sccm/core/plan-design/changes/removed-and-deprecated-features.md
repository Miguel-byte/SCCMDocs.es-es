---
title: Funciones obsoletas | Microsoft Docs
description: "Obtenga información sobre las características, los productos y los sistemas operativos que ya no admite System Center Configuration Manager."
ms.custom: na
ms.date: 06/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: ef42d1483053e9a6c502f4ebcae5a231aa6ba727
ms.openlocfilehash: 98fa323cb94013d875e2cea41b80fff8cc75b6b2
ms.contentlocale: es-es
ms.lasthandoff: 07/26/2017

---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Características eliminadas y en desuso de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

En este tema se describen las características, los productos y los sistemas operativos que dejaron de ser compatibles con System Center Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). Se proporcionan notificaciones anticipadas sobre los cambios futuros que puedan afectar a su uso de Configuration Manager.  

Esta información está sujeta a cambios en versiones futuras y puede no incluir todas las características, productos o sistemas operativos en desuso.  

## <a name="how-to-use-this-information"></a>Cómo usar esta información  
Cuando una función o un sistema operativo aparece por primera vez como obsoleto, se programa para que se quite la compatibilidad para el uso con Configuration Manager en una versión futura de Configuration Manager. Esta información se proporciona para ayudarle a planear alternativas al uso de dicha función o sistema operativo. Cuando se publique la primera versión de Configuration Manager en la que se ha quitado la compatibilidad, este tema se actualizará para indicar la versión específica.  

Cuando se quita la compatibilidad con una función o un sistema operativo, la función o el sistema operativo siguen siendo compatibles cuando se usa una versión anterior de Configuration Manager, siempre y cuando dicha versión de Configuration Manager siga siendo compatible. Sin embargo, cuando se utiliza una versión de Configuration Manager publicada después de la fecha o la versión indicada, esa versión de Configuration Manager no ofrece compatibilidad.

Por ejemplo, si se programó quitar la compatibilidad con una función en la primera actualización publicada después de septiembre de 2016, la compatibilidad con dicha función dejaría de estar incluida en la actualización 1610, que se publicó en octubre de 2016.
-  Con la actualización 1610, la función ya no es compatible.
-  Este tema se actualizaría para indicar que la compatibilidad se quitó con la versión 1610.
Sin embargo, si sigue usando una versión anterior que admite la función, como la versión 1602 o 1606, puede seguir usando la función hasta que la versión que usa deje de ser compatible.

Para obtener más información, vea:
 - Sitio web de la [directiva de ciclos de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).
 - [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemas operativos en desuso
### <a name="server-operating-systems"></a>Sistemas operativos de servidor  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado** |  
|-|-|-|  
|Windows Server 2008|10 de julio de 2015|Versión 1511 </br></br>Se quitó la compatibilidad como un sistema de sitio. (Vea la nota 1).|  
|Windows Server 2008 R2|10 de julio de 2015| Versión 1702 (véase la nota 2)|  

-   Nota 1: No se admite este sistema operativo para servidores de sitio o roles de sistema de sitio con la excepción del punto de distribución y el punto de distribución de extracción. Puede seguir usando este sistema operativo como un punto de distribución hasta que se anuncie que esta compatibilidad queda obsoleta o expire el período extendido de soporte técnico de este sistema operativo. Para más información, vea [Installation of System Center Configuration Manager CB and LTSB fails on Windows Server 2008](https://support.microsoft.com/help/4015095) (La instalación de System Center Configuration Manager CB y LTBS produce un error en Windows Server 2008).

-   Nota 2: a partir de la versión 1702, este sistema operativo no se admite para los servidores de sitio o la mayoría de los roles de sistema de sitio; sin embargo, las versiones anteriores a 1702 sí permitirán utilizarlo. Este sistema operativo se seguirá admitiendo para el rol de sistema de sitio del punto de distribución (incluidos los puntos de distribución de extracción, así como para el entorno PXE y multidifusión) hasta que se anuncie que esta compatibilidad está en desuso o hasta que expire el período extendido de soporte técnico de este sistema operativo. A partir de la versión 1602, puede actualizar in situ el sistema operativo de un servidor de sitio de Windows Server 2008 R2 a Windows Server 2012 R2.  

     Para obtener más información sobre la actualización local de un sistema operativo de servidores de sitio, consulte la sección [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) (Actualización local del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2) del tema [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Cambios introducidos en System Center Configuration Manager).



### <a name="client-operating-systems"></a>Sistemas operativos de cliente  

 A menos que se indique lo contrario, cada uno de los sistemas operativos admitidos como clientes de Configuration Manager seguirá siendo compatible hasta la fecha de finalización de soporte extendido de dicho sistema operativo. Para obtener más información sobre las fechas de finalización de soporte extendido, consulte el [ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle). Si la compatibilidad de Configuration Manager con un sistema operativo termina antes de la fecha de finalización de soporte extendido, aquí se indicará la fecha de desuso y la fecha de fin de soporte para ese sistema operativo.  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Windows XP|10 de julio de 2015|Versión 1511|  
|Windows XP Embedded|10 de julio de 2015|Versión 1702|  
|Windows Server 2003|10 de julio de 2015|Versión 1511|  
|Windows Server 2003 R2|10 de julio de 2015|Versión 1511|  
|Windows Vista|10 de julio de 2015|Versión 1511|  
|Mac OS X  10.6 - 10.8|10 de julio de 2015|Versión 1511|  
|Windows Mobile 6.0 - 6.5|10 de julio de 2015|Versión 1511|  
|Nokia Symbian Belle|10 de julio de 2015|Versión 1511|  
|Windows CE 5.0 - 6.0|10 de julio de 2015|Versión 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Compatibilidad en desuso con versiones de SQL Server como base de datos de sitio  

|**Versiones de SQL Server**|**Primer anuncio del desuso**|**Soporte eliminado**|   
|-|-|-|  
|SQL Server 2008|10 de julio de 2015|Versión 1511|  
|SQL Server 2008 R2|10 de julio de 2015|Versión 1702|  

Si necesita actualizar la versión de SQL Server, se recomiendan los métodos siguientes, del más sencillo al más complicado.
1. [Realice una actualización local de SQL Server](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recomendado).
2. Instale una nueva versión de SQL Server en un equipo nuevo y después [use la opción para mover datos](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) del programa de instalación de Configuration Manager para transfiera el servidor de sitio a la nueva instancia de SQL Server.
3. Use [Copia de seguridad y recuperación](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Características en desuso  

|**Característica**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|10 de julio de 2015|Versión 1511|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|16 de octubre de 2015|Versión 1511|
|Secuencias de tareas: <br /> - OSDPreserveDriveLetter  <br /><br /> Ahora, durante una implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:). Si quiere especificar otra unidad, puede cambiar la ubicación en el paso de secuencia de tareas Aplicar el sistema operativo. Vaya al valor **Seleccione la ubicación en la que desea aplicar este sistema operativo**, seleccione **Letra de unidad lógica específica** y elija la unidad que quiere usar. |20 de junio de 2016 |Versión 1606 |
|Secuencias de tareas: <br /> - Convertir el disco en dinámico <br /> - Instalar herramientas de implementación |18 de noviembre de 2016|La compatibilidad con estas secuencias de tareas finaliza con la primera actualización publicada después del 1 de junio de 2017.|
|El Centro de software tiene un aspecto renovado y moderno. Las aplicaciones que solo se hubiesen mostrado en el catálogo de aplicaciones que depende de Silverlight (aplicaciones disponibles para el usuario) ahora se muestran en la pestaña **Aplicaciones** del Centro de software. Todavía se puede acceder al catálogo de aplicaciones mediante el vínculo de la pestaña **Estado de la instalación** del Centro de software.<br><br>En los próximos meses, la versión anterior del Centro de software dejará de estar disponible.<br><br>Puede configurar los clientes para que usen el nuevo Centro de software. Para ello, habilite la opción de cliente **Agente de equipo** > **Use new Software Center** (Usar el nuevo Centro de software).<br><br>Para más información sobre el Centro de software, consulte [Planear y configurar la administración de aplicaciones en System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 de diciembre de 2016|La compatibilidad con la versión anterior del Centro de software finaliza con la primera actualización publicada después del 1 de enero de 2018.|
|Administración de discos duros virtuales (VHD) con Configuration Manager. </br></br>Esto incluye la eliminación de opciones para crear un nuevo VHD o administrar un VHD con una secuencia de tareas, y la eliminación del nodo de discos duros virtuales de la consola de Configuration Manager. </br></br>Cuando se quita esta compatibilidad, los VHD existentes no se eliminarán, pero ya no se podrá obtener acceso a ellos desde dentro de la consola de Configuration Manager.  |6 de enero de 2017 |La compatibilidad con VHD finaliza con la primera actualización publicada después del 1 de junio de 2017.|
|Herramienta de evaluación de actualizaciones de System Center Configuration Manager. </br></br>La Herramienta de evaluación de actualizaciones depende de System Center Configuration Manager y del kit de herramientas de compatibilidad de aplicaciones (ACT) 6.x. La versión final de ACT se ha entregado en Windows 10 v1511 ADK. Como no habrá más actualizaciones para ACT, se interrumpirá el soporte para la Herramienta de evaluación de actualizaciones. </br></br>La Herramienta de evaluación de actualizaciones se reemplaza por la característica [Preparación de actualización](/sccm/core/clients/manage/upgrade/upgrade-analytics). El aviso de desuso se agregó a la [página de descarga de la Herramienta de evaluación de actualizaciones](https://www.microsoft.com/download/details.aspx?id=37145) el 12 de septiembre de 2016. |12/9/2016  | 11 de julio de 2017 |  


<br></br>
Detalles adicionales sobre las características eliminadas con la versión 1511 de System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Administración fuera de banda  
 Con Configuration Manager, se ha quitado la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager.  

-   Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). El complemento permite el acceso a las funciones más recientes para administrar AMT, a la vez que elimina las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios.  

-   La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio.  

###  <a name="bkmk_nap"></a> Protección de acceso a redes  
 System Center Configuration Manager ha eliminado la compatibilidad con Protección de acceso a redes. La característica quedó en desuso en Windows Server 2012 R2 y se eliminó en Windows 10.  

 Para alternativas de protección de acceso a redes, consulte la sección *Funcionalidad en desuso* de [Información general sobre servicios de acceso y directivas de redes](https://technet.microsoft.com/library/hh831683.aspx).

