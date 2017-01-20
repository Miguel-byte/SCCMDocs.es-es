---
title: "Características en desuso | System Center Configuration Manager"
description: "Obtenga información sobre las características, los productos y los sistemas operativos que ya no admite System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Características eliminadas y en desuso de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En este tema se describen las características, los productos y los sistemas operativos que dejaron de ser compatibles con System Center Configuration Manager o que dejarán de serlo en una actualización futura (en desuso). Está diseñado para proporcionar advertencias anticipadas acerca de los cambios futuros que puedan afectar a su uso de Configuration Manager.  

 Esta información está sujeta a cambios en versiones futuras y puede no incluir todas las características, los productos o sistemas operativos en desuso.  

## <a name="deprecated-features-products-and-operating-systems"></a>Características, productos y sistemas operativos en desuso  
 Los productos y los sistemas operativos de Microsoft que se muestran como en desuso se encuentran en soporte extendido o bien alcanzaron el final de su ciclo de vida. Los productos y los sistemas operativos de Microsoft que se muestran como en desuso se siguen probando con las versiones actuales de Configuration Manager hasta que superan su ciclo de vida de soporte técnico de Microsoft.  Para obtener más información, consulte el sitio web [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle) .  

 **Características en desuso:**  


|**Característica**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|7/10/2015|√|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|10/16/2015|√|  

 **Sistemas operativos de servidor en desuso:**  

 |**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Windows Server 2008|7/10/2015|La compatibilidad termina con la primera actualización publicada después del 31/12/2016 (véase la nota 1)|  
|Windows Server 2008 R2|7/10/2015|La compatibilidad termina con la primera actualización publicada después del 31/12/2016 (véase la nota 2)|  

-   Nota 1: Una vez finalizado el soporte técnico, este sistema operativo ya no se admitirá para servidores de sitio o la mayoría de los roles de sistema de sitio. No obstante, seguirá admitiendo el rol de sistema de sitio de punto de distribución (incluido el punto de distribución de extracción) hasta que se anuncie que esta compatibilidad está en desuso o expire el período extendido de soporte técnico de este sistema operativo.  

-   Nota 2: Una vez finalizado el soporte técnico, este sistema operativo ya no se admitirá para servidores de sitio o la mayoría de los roles de sistema de sitio. No obstante, sí se admitirá para el punto de migración de estado y el rol de sistema de sitio (incluidos los puntos de distribución de extracción, así como para PXE y multidifusión) hasta que se anuncie el fin de esta compatibilidad y finalice el período de soporte extendido del sistema operativo.  A partir de la versión 1602, puede actualizar in situ el sistema operativo de un servidor de sitio de Windows Server 2008 R2 a Windows Server 2012 R2.  

     Para obtener más información sobre la actualización local de un sistema operativo de servidores de sitio, consulte la sección [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) (Actualización local del sistema operativo de los servidores del sitio que ejecutan Windows Server 2008 R2) del tema [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Cambios introducidos en System Center Configuration Manager).



 **Sistemas operativos cliente en desuso:**  

 A menos que se indique lo contrario, cada uno de los sistemas operativos admitidos como clientes de Configuration Manager seguirá siendo compatible hasta la fecha de finalización de soporte extendido de dicho sistema operativo, tal y como se detalla en [Ciclo de vida de soporte técnico de Microsoft](https://support.microsoft.com/lifecycle).  Si la compatibilidad de Configuration Manager con un sistema operativo termina antes de la fecha de finalización de soporte extendido, aquí se indicará la fecha de desuso y la fecha de fin de soporte para ese sistema operativo.  

|**Sistemas operativos**|**Primer anuncio del desuso**|**Soporte eliminado**|  
|-|-|-|  
|Windows XP|7/10/2015|√|  
|Windows XP Embedded|7/10/2015|El soporte técnico termina con la primera actualización publicada después del 31/12/2016|  
|Windows Server 2003|7/10/2015|√|  
|Windows Server 2003 R2|7/10/2015|√|  
|Windows Vista|7/10/2015|√|  
|Mac OS X  10.6 - 10.8|7/10/2015|√|  
|Windows Mobile 6.0 - 6.5|7/10/2015|√|  
|Nokia Symbian Belle|7/10/2015|√|  
|Windows CE 5.0 - 6.0|7/10/2015|√|  


 **Soporte en desuso para versiones de SQL Server como base de datos de sitio:**  

|**Versiones de SQL Server**|**Primer anuncio del desuso**|**Soporte eliminado**|   
|-|-|-|  
|SQL Server 2008|7/10/2015|√|  
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



<!--HONumber=Nov16_HO1-->


