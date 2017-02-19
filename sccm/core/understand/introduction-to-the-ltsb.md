---
title: "Introducción a la Rama de mantenimiento a largo plazo | Microsoft Docs"
description: "Obtenga información sobre la rama de mantenimiento a largo plazo de System Center Configuration Manager."
ms.custom: na
ms.date: 1/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: a86546eb513a2ef6f95013178b141fb1833ea8ab
ms.openlocfilehash: fa4d7dd2e1edbbc0b136ebfc27560f20ab63c12e


---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Introducción a la rama de mantenimiento a largo plazo de System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Use este tema para obtener información sobre la rama de mantenimiento a largo plazo (LTSB) de Configuration Manager y entender la documentación de esta rama.


La LTSB es una rama distinta de Configuration Manager que se basa en la versión 1606 de la rama actual. Comparada con la rama actual, la LTSB tiene una [funcionalidad reducida](#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Se ha diseñado para clientes que han [permitido que su Software Assurance (SA) o derechos de suscripción equivalentes expiren](/sccm/core/understand/learn-more-editions#software-assurance-and-the-ltsb).

**Introducción a las licencias:**   
Los clientes con Software Assurance (SA) activo en licencias de System Center Configuration Manager o con derechos de suscripción equivalentes el 1 de octubre de 2016, tienen derecho a usar la versión 1606 de octubre de 2016 de System Center Configuration Manager. Los clientes con derechos para System Center Configuration Manager el 1 de octubre de 2016 o después de esta fecha encontrarán dos opciones de licencia tras la instalación: la rama actual y la rama de mantenimiento a largo plazo (LTSB).

**Detalles de las licencias:**  
[Aquí puede encontrar los términos y condiciones completos de los productos que compra mediante los programas de licencias por volumen de Microsoft](http://go.microsoft.com/fwlink/?LinkId=800052).

Los clientes que tengan derechos perpetuos en System Center Configuration Manager, o que admitan que SA o la suscripción expiren después del 1 de octubre, pueden instalar la versión de LTSB de System Center Configuration Manager actual en el momento de caducidad.
- Para obtener información sobre Software Assurance y los requisitos de licencia para System Center Configuration Manager, consulte [System Center Configuration Manager licensing and branches (Ramas y licencias de System Center Configuration Manager)](learn-more-editions.md).
-   Para obtener información sobre las diferencias entre las diferentes ramas, consulte [Which branch of Configuration Manager should I use (Qué rama de Configuration Manager debo usar)](which-branch-should-i-use.md).

Para instalar un sitio o una actualización nueva de un sitio compatible de System Center 2012 Configuration Manager con la LTSB, use el medio de línea base de la versión 1606. Este medio de línea base está disponible en DVD como parte de Microsoft System Center 2016 o de una versión de System Center Configuration Manager (rama actual y rama de mantenimiento a largo plazo 1606). El medio de línea base que puede instalar la LTSB también puede usarse para instalar la versión 1606 de la rama actual de Configuration Manager. Para obtener información sobre el medio de línea base, consulte [Versiones de actualización y línea base](/sccm/core/servers/manage/updates#baseline-and-update-versions).

Para obtener información sobre cómo instalar un sitio de LTSB, consulte [Install and Upgrade for the Long-Term Servicing Branch (Instalar y actualizar la rama de mantenimiento a largo plazo)](install-the-ltsb.md). Consulte la [documentación de System Center 2016](https:\technet.microsoft.com\system-center-docs\System-Center-2016) para obtener información sobre cómo obtener System Center 2016.

> [!IMPORTANT]
> Todos los sitios de la jerarquía deben ejecutar la misma rama. Tener una jerarquía con una mezcla de LTSB y rama actual en diferentes sitios no se admite.
>
> De la misma manera, cuando usa la recuperación, debe restaurar el sitio o la base de datos del sitio a su rama original. No puede recuperar una base de datos del sitio de la rama actual a una instalación de LTSB, o viceversa.


## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Características que no están disponibles en la LTSB de Configuration Manager
En comparación con la rama actual, la LTSB tiene las siguientes limitaciones de compatibilidad:

- No recibe actualizaciones de nuevas características
- No admite la adición de una suscripción a Microsoft Intune, que impide el uso de:
  - Intune en una configuración de administración de dispositivos móviles (MDM) híbrida
  - MDM local
-   No admite el uso del panel de mantenimiento de Windows 10, los planes de mantenimiento y no admite la rama actual de Windows 10 (CB) y la rama actual para empresas (CBB).
- No admite las versiones futuras de Windows 10 LTSB y Windows Server
-   No admite Asset Intelligence
-   No admite puntos de distribución basados en la nube
-   No admite la compatibilidad con Exchange Online como Exchange Connector
-   No admite ninguna característica de versión preliminar


Aunque la compatibilidad con estas características no se incluye en la LTSB, algunas características permanecen visibles en la consola de Configuration Manager, pero no pueden seleccionarse o usarse.

Además, los nuevos sistemas operativos que se agregan como compatibles con la rama actual no serán compatibles con la LTSB.

## <a name="documentation-for-the-ltsb"></a>Documentación de la LTSB
Como la LTSB se basa en la rama actual de la versión 1606, la documentación que usa para la LTSB es la [documentación en línea que se aplica a la rama actual](https://docs.microsoft.com/sccm/), con las salvedades y limitaciones específicas de la LTSB como se identifica en los siguientes temas:  

-   [Introducción a la rama de mantenimiento a largo plazo](introduction-to-the-ltsb.md) (este tema).

-   [¿Qué rama de Configuration Manager debo utilizar?](which-branch-should-i-use.md): información sobre las diferentes ramas de System Center Configuration Manager, de manera que pueda estar seguro de instalar la mejor rama para sus necesidades.

-   [Instalar la rama de mantenimiento a largo plazo](install-the-ltsb.md): cómo instalar un nuevo sitio de LTSB o actualizar un sitio de System Center 2012 Configuration Manager a la LTSB.

-   [Actualizar la rama de mantenimiento a largo plazo a la rama actual](convert-to-current-branch.md): cómo convertir la instalación de LTSB en una instalación de rama actual.

-   [Licencias y ramas para System Center Configuration Manager](learn-more-editions.md): información sobre Software Assurance y requisitos de licencia relacionados para System Center Configuration Manager.
-   [Configuraciones admitidas de la rama de mantenimiento a largo plazo ](supported-configurations-for-ltsb.md): las versiones y los requisitos para el sistema operativo y los productos dependientes como SQL Server que puede usar con la LTSB.


Para ayudarle a distinguir qué documentación específica de rama se aplica, use la guía siguiente:  
-   Los temas con el encabezado *Se aplica a: rama actual*, se aplican tanto a la rama actual como a la rama de mantenimiento a largo plazo (aunque algunas partes del tema puede que solo se apliquen a una versión más reciente de la rama actual).

-   Para identificar las partes de un tema que no se aplican a la LTSB, las características y los cambios que se presentaron después de la versión 1606 de la rama actual se identifican con palabras como *A partir de la versión 1610*. Como estos se presentaron después de la versión 1606 de la rama actual, no están disponibles en la LTSB.

### <a name="similarities-between-the-current-branch-and-the-ltsb"></a>Similitudes entre la rama actual y la LTSB
Como la LTSB se basa en la versión 1606 de la rama actual (con algunas excepciones como las características relacionadas con la nube y la integración de Intune), la mayoría de las tareas empleadas en la planeación de la implementación, la configuración y la administración de las dos ramas son idénticas.

Por ejemplo, la LTSB admite el mismo número de sitios, tipos de sitio, clientes e infraestructura general que la rama actual. Por lo tanto, use la guía que se encuentra en el sitio, y los temas de diseño y planeación de jerarquías para la rama actual. Asimismo, para las características que son compatibles con ambas ramas como Actualizaciones de software o Implementación de sistema operativo, use la guía que se encuentra en esas secciones de la documentación de la rama actual con las advertencias de no tener acceso a los cambios que se han presentado después de la versión 1606 de la rama actual.


## <a name="how-to-identify-your-branch-and-version"></a>Cómo identificar la rama y la versión
Cuando ve la información de la versión de un sitio de Configuration Manager, también confirma la rama.

Para comprobar la versión del sitio, en la esquina superior izquierda de la consola, vaya a **Acerca de System Center Configuration Manager**, donde aparece la **versión del sitio** como **5.0.8412.1000**.

Para confirmar la rama del sitio (como LTSB o rama actual), en la consola, vaya a **Administración** > **Configuración de sitio** > **Sitios** y abra **Configuración de jerarquía**.  Si existe una opción de conversión a la rama actual y está activa, el sitio ejecuta la versión de LTSB. Cuando el sitio ejecuta la rama actual, está opción aparece atenuada.

Para más información sobre las diferentes versiones de Configuration Manager, vea "Versiones de línea de base y versiones de actualización" en el tema [Actualizaciones para System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="exceptions-for-using-the-ltsb"></a>Excepciones para usar la LTSB
### <a name="updates-and-servicing-of-the-ltsb"></a>Actualizaciones y mantenimiento de la LTSB
Solo las actualizaciones de seguridad imprescindibles están disponibles como actualizaciones en la consola en la LTSB.

La información sobre las actualizaciones periódicas para las versiones de rama actual posteriores está visible en la consola, pero no para la LTSB. No se descargan y no se pueden instalar.

Para admitir las actualizaciones en la consola para correcciones de seguridad imprescindibles, un sitio de LTSB requiere el uso del [punto de conexión de servicio](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Puede configurar este rol de sistema de sitio en modo en línea o sin conexión, como se realiza para la rama actual. La LTSB recopila y envía los mismos datos de uso y telemetría que la rama actual.

La LTSB admite el uso del instalador de la revisión y la herramienta de registro de actualizaciones, como se documenta para la rama actual.

Para obtener información general sobre las actualizaciones y el mantenimiento, consulte [Updates for Configuration Manager (Actualizaciones para Configuration Manager)](/sccm/core/servers/manage/updates).

### <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Cambios para la expansión del sitio y la carpeta CD.Latest
Cuando ejecute la LTSB y esté expandiendo un sitio primario independiente mediante la instalación de un nuevo sitio de administración central, debe usar el programa de instalación y los archivos de origen del medio de línea base de la versión 1606.  Para la rama actual, ejecute el programa de instalación y use los archivos de origen de la carpeta CD.Latest.

Aunque no ejecute el programa de instalación para la expansión de sitios de la carpeta CD.Latest, siga usando la carpeta CD.Latest para la recuperación de sitios y para instalar un nuevo sitio principal secundario cuando su primer sitio de LTSB era un sitio de administración central.

Para obtener más información, consulte [Expandir un sitio primario independiente](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site) en [Use the Setup Wizard to install sites (Usar el Asistente para instalación para instalar sitios)](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).
Para obtener más información sobre la carpeta CD.Latest, consulte [La carpeta CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).



<!--HONumber=Jan17_HO2-->


