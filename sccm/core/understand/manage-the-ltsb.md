---
title: Administración de LTSB
titleSuffix: Configuration Manager
description: Diferencias de administración de la LTSB de System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08ab6cebbe44ecad8b8ce15691dd83217ada3ce9
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194133"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Administrar la rama de mantenimiento a largo plazo de Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama de mantenimiento a largo plazo)*

La información siguiente puede ayudarle a comprender cambios importantes que afectan al modo en que se administra la infraestructura al usar la rama de mantenimiento a largo plazo (LTSB) de System Center Configuration Manager.

Como la LTSB es equivalente a la versión 1606 de la rama actual (con algunas excepciones como las características relacionadas con la nube y la integración de Intune), la mayoría de las tareas empleadas en la planeación de la implementación, la configuración y la administración son iguales.

Por ejemplo, la LTSB admite el mismo número de sitios, tipos de sitio, clientes e infraestructura general que la rama actual. Por lo tanto, use la guía que se encuentra en el sitio, y los temas de diseño y planeación de jerarquías para la rama actual. Asimismo, para las características con la LSTB que son compatibles con ambas ramas como, por ejemplo, Actualizaciones de software o Implementación de sistema operativo, use la guía que se encuentra en esas secciones de la documentación de la rama actual con las advertencias de no tener acceso a cambios de características presentados después de la versión 1606 de la rama actual.

En las secciones siguientes se ofrece información sobre tareas de administración que no son similares.

## <a name="updates-and-servicing"></a>Actualizaciones y mantenimiento
Solo las actualizaciones de seguridad imprescindibles están disponibles como actualizaciones en la consola en la LTSB.  

La información sobre las actualizaciones periódicas para las versiones de rama actual posteriores está visible en la consola, pero no para la LTSB. No se descargan y no se pueden instalar.

Para admitir las actualizaciones en la consola para correcciones de seguridad imprescindibles, un sitio de LTSB requiere el uso del [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Puede configurar este rol de sistema de sitio en modo en línea o sin conexión, como se realiza para la rama actual. La LTSB recopila y envía los mismos datos de uso y telemetría que la rama actual.

La LTSB admite el uso del instalador de la revisión y la herramienta de registro de actualizaciones, como se documenta para la rama actual.

Para obtener información general sobre las actualizaciones y el mantenimiento, consulte [Updates for Configuration Manager (Actualizaciones para Configuration Manager)](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Cambios para la expansión del sitio y la carpeta CD.Latest
Cuando ejecute la LTSB y esté expandiendo un sitio primario independiente mediante la instalación de un nuevo sitio de administración central, debe usar el programa de instalación y los archivos de origen del medio de línea base de la versión 1606. Para la rama actual, ejecute el programa de instalación y use los archivos de origen de la carpeta CD.Latest.

Aunque no ejecute el programa de instalación para la expansión de sitios de la carpeta CD.Latest, siga usando la carpeta CD.Latest para la recuperación de sitios y para instalar un nuevo sitio principal secundario cuando su primer sitio de LTSB era un sitio de administración central.

Para obtener más información sobre la expansión de sitios, vea [Use el Asistente para instalación si quiere instalar sitios de System Center Configuration Manager](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand). Para obtener más información sobre la carpeta CD.Latest, consulte [La carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Recuperación
Cuando recupera un sitio, debe restaurar el sitio o la base de datos del sitio a su rama original. No puede recuperar una base de datos del sitio de la rama actual a una instalación de LTSB, o viceversa.
