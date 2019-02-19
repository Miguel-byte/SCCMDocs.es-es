---
title: Introducción a la rama de mantenimiento a largo plazo
titleSuffix: Configuration Manager
description: Obtenga información sobre la rama de mantenimiento a largo plazo de System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f714be298c244b86178780138f5a700c89ae2a76
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128990"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introducción a la rama de mantenimiento a largo plazo de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama de mantenimiento a largo plazo)*

La rama de mantenimiento a largo plazo (LTSB) de System Center Configuration Manager es una rama distinta de Configuration Manager que se ha diseñado como opción de instalación disponible para todos los clientes. Pero se trata de la única opción para clientes que dejen caducar sus derechos de suscripción de Software Assurance (SA) o equivalente para Configuration Manager.


Con respecto a la versión 1606 de Configuration Manager, la LTSB tiene menor funcionalidad cuando se compara con la rama actual de Configuration Manager.

 > [!TIP]   
 > Si desea obtener información sobre las ramas de **Windows Server**, vea [Windows Server 2016 new Current Branch for Business servicing option]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Nueva rama actual de Windows Server 2016 para la opción de mantenimiento empresarial).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Características que no están disponibles en la LTSB de Configuration Manager
La rama actual de Configuration Manager admite la funcionalidad siguiente que no está disponible cuando se usa la LTSB:

-   Actualizaciones en consola que agregan nueva funcionalidad y mejoras.
-   Compatibilidad con sistemas operativos recién publicados que se usen como clientes y servidores de sitio.
-   Uso de una suscripción de Microsoft Intune que admita:
    -   Intune en una configuración de administración de dispositivos móviles (MDM) híbrida
    -   MDM local
-   El panel de mantenimiento de Windows 10 y los planes de mantenimiento, incluida la compatibilidad con versiones recientes de la rama actual de Windows 10 (CB) y la rama actual para empresas (CBB).  
-   Compatibilidad con versiones futuras de Windows 10 LTSB y Windows Server
-   Asset Intelligence
-   Puntos de distribución basados en la nube
-   Exchange Online como Exchange Connector    

Aunque la compatibilidad con estas características no está disponible en la LTSB, algunas características permanecen visibles en la consola de Configuration Manager, pero no se pueden seleccionar ni usar.


## <a name="find-documentation-for-the-ltsb"></a>Buscar documentación de la LTSB
La LTSB se basa en la versión 1606 de la rama actual. Para obtener documentación del producto, use la [documentación de la rama actual](https://docs.microsoft.com/sccm/), con advertencias y limitaciones que son específicas de la LTSB. Estas advertencias y limitaciones se identifican en los temas en línea siguientes:

- [Introducción a la rama de mantenimiento a largo plazo](introduction-to-the-ltsb.md): (En este tema)
- [Instalar y actualizar con el medio de línea base de la versión 1606 para System Center Configuration Manager](install-the-ltsb.md)
- [Actualizar la rama de mantenimiento a largo plazo a la rama actual](convert-to-current-branch.md)
- [Configuraciones admitidas para la rama de mantenimiento a largo plazo](supported-configurations-for-ltsb.md)
- [Administrar la rama de mantenimiento a largo plazo de Configuration Manager](manage-the-ltsb.md)

Cuando se hace referencia a la documentación de la rama actual sobre la LTSB, los detalles que se aplican a la versión 1606 también se aplican a la LTSB. Las características o los detalles que se presentan con la versión 1610 o versiones posteriores no se admiten en la LTSB.


## <a name="licensing-overview-for-the-ltsb"></a>Introducción a las licencias para la LTSB   
Los clientes con Software Assurance (SA) activo en licencias de System Center Configuration Manager o con derechos de suscripción equivalentes el 1 de octubre de 2016, tienen derecho a usar la versión 1606 de octubre de 2016 de System Center Configuration Manager. Los clientes con derechos para System Center Configuration Manager el 1 de octubre de 2016 o después de esta fecha encontrarán dos opciones con licencia tras la instalación: Rama actual y Rama de mantenimiento a largo plazo (LTSB).

Los clientes que tengan derechos perpetuos en System Center Configuration Manager, o que admitan que SA o la suscripción expiren después del 1 de octubre, pueden instalar la versión de LTSB de System Center Configuration Manager actual en el momento de caducidad.

[Aquí puede encontrar los términos y condiciones completos de los productos que compra mediante los programas de licencias por volumen de Microsoft](http://go.microsoft.com/fwlink/?LinkId=800052).

Para obtener más información sobre licencias para ramas de Configuration Manager, vea [Licencias y ramas para System Center Configuration Manager](learn-more-editions.md).

## <a name="next-steps"></a>Pasos siguientes

Si decide que la LTSB de Configuration Manager es la rama adecuada para su entorno, [instale un nuevo sitio de LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) como parte de una nueva jerarquía o [actualice un sitio de System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) y la jerarquía.

Si no dispone de medios de instalación, vea la [documentación de System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) para obtener información sobre cómo obtener System Center 2016, que incluye medios que puede usar para instalar la LSTB de System Center Configuration Manager.  
