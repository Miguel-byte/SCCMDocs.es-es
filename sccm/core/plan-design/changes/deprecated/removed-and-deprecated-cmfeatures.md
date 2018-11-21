---
title: Características en desuso
titleSuffix: Configuration Manager
description: Obtenga información sobre las características que Configuration Manager ya no admite.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c1e07a2911a5f8560e3b69d7596716eb526bb34
ms.sourcegitcommit: 3772ece83823714b2aae46ec20523cc094701760
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681433"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Características en desuso y eliminadas de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Este artículo enumera las características que están en desuso o no reciben soporte técnico de Configuration Manager. Las características en desuso se van a quitar en una futura actualización. Estos cambios futuros podrían afectar al uso de Configuration Manager.  

Esta información está sujeta a cambios en futuras versiones. Podría no incluir todas las características de Configuration Manager en desuso.



## <a name="deprecated-features"></a>Características en desuso  

|Característica|Primer anuncio del desuso|Soporte técnico eliminado|  
|-----------|---|--------------|  
|System Center Endpoint Protection para Mac y Linux<br>Para obtener más información, vea la [entrada del blog de fin del soporte técnico](https://go.microsoft.com/fwlink/?linkid=870182).|Octubre de 2018|31 de diciembre de 2018|
|Administración híbrida de dispositivos móviles. Para más información, vea [¿Qué es la Administración híbrida de dispositivos móviles (MDM)?](/sccm/mdm/understand/hybrid-mobile-device-management). <!--Intune feature 2683117-->|14 de agosto de 2018|1 de septiembre de 2019|
|La **experiencia de usuario de Silverlight** del punto de sitios web del catálogo de aplicaciones ya no se admite. Los usuarios deben utilizar el nuevo Centro de software. NOTA: Los roles Punto de sitios web y Punto de servicio web del catálogo de aplicaciones todavía son compatibles. En algunos escenarios, el nuevo Centro de software se comunica con el punto de sitio web del catálogo de aplicaciones. Para obtener más información, consulte [Configurar el centro de software](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).<!--1358309-->|11 de agosto de 2017| Versión 1806|
|La versión anterior del Centro de software.<br><br>Para obtener más información sobre el nuevo Centro de software, vea [Planear y configurar la administración de aplicaciones](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|13 de diciembre de 2016|Versión 1802|
|Administración de discos duros virtuales (VHD) con Configuration Manager. </br></br>Este desuso incluye la eliminación de opciones para crear un nuevo VHD o administrar un VHD con una secuencia de tareas, y la eliminación del nodo de discos duros virtuales de la consola de Configuration Manager. </br></br>Los VHD existentes no se eliminan, pero ya no son accesibles desde la consola de Configuration Manager.  |6 de enero de 2017 |Versión 1710|
|Secuencias de tareas: <br /> - Convertir el disco en dinámico <br /> - Instalar herramientas de implementación |18 de noviembre de 2016|Versión 1710|
|Herramienta de evaluación de actualizaciones de System Center Configuration Manager. </br></br>La Herramienta de evaluación de actualizaciones depende de System Center Configuration Manager y del kit de herramientas de compatibilidad de aplicaciones (ACT) 6.x. La versión final de ACT se ha entregado en Windows 10 v1511 ADK. Como no hay más actualizaciones para ACT, se interrumpe el soporte para la Herramienta de evaluación de actualizaciones. </br></br>La Herramienta de evaluación de actualizaciones se reemplaza por la característica [Preparación de actualización](/sccm/core/clients/manage/upgrade/upgrade-analytics). El aviso de desuso se agregó a la [página de descarga de UAT](https://www.microsoft.com/download/details.aspx?id=37145) el 12 de septiembre de 2016. | 12 de septiembre de 2016  | 11 de julio de 2017 |
|Puntos de actualización de software con un clúster de equilibrio de carga de red (NLB) | 27 de febrero de 2016 | Versión 1702 | 
|Secuencias de tareas: <br /> - OSDPreserveDriveLetter  <br /><br /> Ahora, durante una implementación del sistema operativo, el programa de instalación de Windows determina, de forma predeterminada, cuál es la mejor letra de unidad (normalmente C:). Si quiere especificar otra unidad, puede cambiar la ubicación en el paso de secuencia de tareas Aplicar el sistema operativo. Vaya a la opción de configuración **Seleccionar la ubicación en la que desea aplicar este sistema operativo**. Seleccione **Letra de unidad lógica específica** y elija la unidad que desee utilizar. |20 de junio de 2016 |Versión 1606 |
|Protección de acceso a redes (NAP): como aparece en System Center 2012 Configuration Manager|10 de julio de 2015|Versión 1511|  
|Administración fuera de banda: como aparece en System Center 2012 Configuration Manager|16 de octubre de 2015|Versión 1511|



## <a name="features-removed-in-version-1511"></a>Características eliminadas de la versión 1511
Las secciones siguientes incluyen detalles adicionales de las características eliminadas con la versión 1511:

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
 - [Directiva de ciclo de vida de Microsoft](https://support.microsoft.com/lifecycle)
 - [Compatibilidad con versiones de la rama actual de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
