---
title: Funciones obsoletas | Microsoft Docs
description: "Obtenga información sobre las características, los productos y los sistemas operativos que ya no admite System Center Configuration Manager."
ms.custom: na
ms.date: 12/05/2016
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
translationtype: Human Translation
ms.sourcegitcommit: ffebee1e85008611a9841dc849bea735d15a88c6
ms.openlocfilehash: 888b6de9fd2b70e8b4f58e32cca7cf5e615d1dca


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Características eliminadas y en desuso de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema se describen las características, los productos y los sistemas operativos que dejaron de ser compatibles con System Center Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). Está diseñado para proporcionar advertencias anticipadas acerca de los cambios futuros que puedan afectar a su uso de Configuration Manager.  

 Esta información está sujeta a cambios en versiones futuras y puede no incluir todas las características, los productos o sistemas operativos en desuso.  

## <a name="how-to-use-this-information"></a>Cómo usar esta información  
Cuando una función o un sistema operativo aparece por primera vez como obsoleto, se programa para que se quite la compatibilidad para el uso con Configuration Manager en una versión futura de Configuration Manager. Esta información se proporciona para ayudarle a planear alternativas al uso de dicha función o sistema operativo.  Cuando se publique la primera versión de Configuration Manager en la que se ha quitado la compatibilidad, los detalles de este tema se actualizarán para indicar que la versión específica.  

Cuando se quita la compatibilidad con una función o un sistema operativo, el sistema operativo o la función sigue siendo compatible cuando se utiliza una versión anterior de Configuration Manager, siempre y cuando dicha versión de Configuration Manager siga siendo compatible. Sin embargo, cuando se utiliza una versión de Configuration Manager publicada después de la fecha o la versión indicada, esa versión de Configuration Manager no ofrece compatibilidad.

**Por ejemplo:** si se programó una función para quitar la compatibilidad con la primera actualización publicada después de septiembre de 2016, esto implicaría que la compatibilidad para esa función dejaría de estar incluida en la actualización 1610, que se publicó en octubre de 2016.
-  Con la actualización 1610, la función ya no es compatible.
-  Este contenido se actualizaría para indicar que la compatibilidad se quitó con la versión 1610.
Sin embargo, si sigue usando una versión anterior que admite la función, como la versión 1602 o 1606, puede seguir usando la función hasta que la versión que usa deje de ser compatible.

Para obtener más información, vea:
 - Sitio web de la [Directiva del Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle)
 - [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)

**Características en desuso:**  


|**Característica**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|7/10/2015|Versión 1511|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|10/16/2015|Versión 1511|
|Secuencias de tareas: <br /> - Convertir el disco en dinámico <br /> - Instalar herramientas de implementación |18/11/2016|La compatibilidad con estas secuencias de tareas finaliza con la primera actualización publicada después del 1 de junio de 2017|
|El nuevo Centro de software tiene un aspecto novedoso y moderno. Además, las aplicaciones que solo se hubiesen mostrado en el catálogo de aplicaciones que depende de Silverlight (aplicaciones disponibles para el usuario) ahora se muestran en la pestaña **Aplicaciones** del Centro de software. Todavía se puede acceder al catálogo de aplicaciones mediante el vínculo de la pestaña **Estado de la instalación** del centro de software.<br><br>En los próximos meses, quitaremos la versión anterior del Centro de software y ya no podrá usarlo.<br><br>Es posible configurar los clientes para usar el nuevo centro de software mediante la habilitación de la opción de cliente **Agente de equipo** > **Usar el nuevo Centro de software**.<br><br>Para más información sobre el Centro de software, consulte [Planear y configurar la administración de aplicaciones en System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|12/13/2016|Se anunciará| 

 **Sistemas operativos de servidor en desuso:**  

 |**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado** |  
|-|-|-|  
|Windows Server 2008|7/10/2015|La compatibilidad termina con la primera actualización publicada después del 31/12/2016 *(véase la nota 1)*|  
|Windows Server 2008 R2|7/10/2015|La compatibilidad termina con la primera actualización publicada después del 31/12/2016 *(véase la nota 2)*|  

-   *Nota 1*: Una vez finalizado el soporte técnico, este sistema operativo ya no se admitirá para servidores de sitio o la mayoría de los roles de sistema de sitio. No obstante, seguirá admitiendo el rol de sistema de sitio de punto de distribución (incluido el punto de distribución de extracción) hasta que se anuncie que esta compatibilidad está en desuso o expire el período extendido de soporte técnico de este sistema operativo.  

-   *Nota 2*: Una vez finalizado el soporte técnico, este sistema operativo ya no se admitirá para servidores de sitio o la mayoría de los roles de sistema de sitio. No obstante, sí se admitirá para el punto de migración de estado y el rol de sistema de sitio (incluidos los puntos de distribución de extracción, así como para PXE y multidifusión) hasta que se anuncie el fin de esta compatibilidad y finalice el período de soporte extendido del sistema operativo.  A partir de la versión 1602, puede actualizar in situ el sistema operativo de un servidor de sitio de Windows Server 2008 R2 a Windows Server 2012 R2.  

     Para obtener más información sobre la actualización local de un sistema operativo de servidores de sitio, consulte la sección [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) (Actualización local del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2) del tema [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Cambios introducidos en System Center Configuration Manager).



 **Sistemas operativos cliente en desuso:**  

 A menos que se indique lo contrario, cada uno de los sistemas operativos admitidos como clientes de Configuration Manager seguirá siendo compatible hasta la fecha de finalización de soporte extendido de dicho sistema operativo, tal y como se detalla en [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).  Si la compatibilidad de Configuration Manager con un sistema operativo termina antes de la fecha de finalización de soporte extendido, aquí se indicará la fecha de desuso y la fecha de fin de soporte para ese sistema operativo.  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Windows XP|7/10/2015|Versión 1511|  
|Windows XP Embedded|7/10/2015|El soporte técnico termina con la primera actualización publicada después del 31/12/2016|  
|Windows Server 2003|7/10/2015|Versión 1511|  
|Windows Server 2003 R2|7/10/2015|Versión 1511|  
|Windows Vista|7/10/2015|Versión 1511|  
|Mac OS X  10.6 - 10.8|7/10/2015|Versión 1511|  
|Windows Mobile 6.0 - 6.5|7/10/2015|Versión 1511|  
|Nokia Symbian Belle|7/10/2015|Versión 1511|  
|Windows CE 5.0 - 6.0|7/10/2015|Versión 1511|  


 **Soporte en desuso para versiones de SQL Server como base de datos de sitio:**  

|**Versiones de SQL Server**|**Primer anuncio del desuso**|**Soporte eliminado**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|Versión 1511|  
|SQL Server 2008 R2|7/10/2015|El soporte técnico termina con la primera actualización publicada después del 31/12/2016|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Características eliminadas en System Center Configuration Manager  
 Desde la versión inicial de System Center Configuration Manager, se han quitado las siguientes características:

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Administración fuera de banda  
 Con Configuration Manager, se ha quitado la compatibilidad nativa con equipos basados en AMT desde la consola de Configuration Manager.  

-   Los equipos basados en AMT siguen estando totalmente administrados cuando se usa el [complemento Intel SCS para Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html).  

-   El uso del complemento ofrece acceso a las últimas capacidades para administrar AMT a la vez que quita las limitaciones introducidas hasta que Configuration Manager pudo incorporar esos cambios  

-   La administración fuera de banda en System Center 2012 Configuration Manager no se ve afectada por este cambio  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Protección de acceso a redes  
 System Center Configuration Manager ha eliminado la compatibilidad con Protección de acceso a redes. La característica quedó en desuso en Windows Server 2012 R2 y se eliminó en Windows 10.  

 Para alternativas de protección de acceso a redes, consulte la sección **Funcionalidad en desuso** de [Información general sobre servicios de acceso y directivas de redes](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Dec16_HO3-->


