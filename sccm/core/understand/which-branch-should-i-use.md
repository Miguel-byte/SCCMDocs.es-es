---
title: "Qué rama debo usar | Microsoft Docs"
description: "Obtenga información acerca de las diferencias entre las ramas disponibles de System Center Configuration Manager."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 26a362b4e5f25414178cae6843869a54eb99028c
ms.openlocfilehash: b190b6116fba8080ad4e144e4e349e0926d1340b
ms.lasthandoff: 02/28/2017


---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>¿Qué rama de Configuration Manager debo utilizar?

*Se aplica a: System Center Configuration Manager (Rama actual, Rama de mantenimiento a largo plazo y Technical Preview)*


Desde octubre de 2016, hay disponibles tres ramas de System Center Configuration Manager. Use este tema para ayudarle a seleccionar la rama adecuada a sus necesidades.

## <a name="current-branch-of-system-center-configuration-manager"></a>Rama actual de System Center Configuration Manager
Se trata de una rama con licencia para su uso en un entorno de producción donde desea contar con la opción de obtener las características y funcionalidades más recientes. Es la rama que se usa si tiene lo siguiente: System Center Datacenter, System Center Standard, System Center Configuration Manager o derechos de suscripción equivalentes. Para obtener más información sobre Software Assurance y opciones de licencia, consulte [Licencias y ramas para System Center Configuration Manager](learn-more-editions.md).


>  [!TIP]
> La Rama actual también puede instalarse como una versión de evaluación que no requiere una licencia. Puede usarse una versión de evaluación durante 180 días, y admite la actualización a una edición con licencia de la Rama actual.

La Rama actual se actualiza varias veces al año con nuevas características. Cada versión de actualización se admite durante un año tras su publicación. Debe actualizar a una versión más reciente de la Rama actual en ese período de un año o antes de que expire. Las actualizaciones a las versiones más recientes están disponibles como las actualizaciones en la consola.

Para instalar la Rama actual como un sitio nuevo o como una actualización de System Center 2012 Configuration Manager con Service Pack 2 o System Center 2012 R2 Configuration Manager con Service Pack 1, se usan los [medios de línea base](/sccm/core/servers/manage/updates#baseline-and-update-versions) para System Center Configuration Manager que se incluyen como un DVD con System Center 2016 o que están disponibles como parte de una versión independiente de System Center Configuration Manager. El acceso a este medio depende del tipo de licencia que tenga para System Center Configuration Manager.

También se pueden usar los medios de línea base para instalar un nuevo sitio que sea una versión de evaluación de la Rama actual. Si solo quiere instalar una versión de evaluación, puede obtener el software desde el sitio web de [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]
> Use los medios de línea base para instalar sitios para una nueva jerarquía de Configuration Manager. Si ha instalado previamente una versión de línea base como 1511, use las actualizaciones en consola para actualizar los sitios a una nueva versión, como 1606.
>
> Los sitios que se actualizan mediante las actualizaciones en la consola dan lugar a sitios que son iguales que el nuevo sitio instalado mediante los medios de linea base.
>
> Para obtener más información, consulte [Updates for System Center Configuration Manager](/sccm/core/servers/manage/updates) (Actualizaciones para System Center Configuration Manager).

**Características de la Rama actual**
- Recibe [actualizaciones en la consola](/sccm/core/servers/manage/install-in-console-updates) que ponen las características nuevas a disposición de los usuarios.
- Recibe actualizaciones en la consola que ofrecen seguridad y revisiones de calidad para las características existentes.
- Admite actualizaciones de fuera de banda cuando sea necesario. Vea [Uso de la herramienta de registro de actualizaciones](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) o [Uso del instalador de revisiones](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Puede interoperar con Microsoft Intune y otros servicios e infraestructura basados en la nube.
- Admite la [migración de datos](/sccm/core/migration/migrate-data-between-hierarchies) desde y hacia otras instalaciones de Configuration Manager.
- Admite la actualización desde versiones anteriores de Configuration Manager.
- Admite la instalación como versión de evaluación, desde la que más adelante puede actualizar a una instalación con licencia completa.

La versión inicial de la Rama actual era la versión 1511. Entre las actualizaciones posteriores se encuentran las versiones 1602, 1606, etc. Cada versión permanece disponible durante un año, y Microsoft le recomienda que actualice a la versión más reciente poco después de su lanzamiento. Puede esperar hasta un año antes de actualizar a una versión más reciente, y también puede omitir una actualización para instalar la versión más reciente disponible. Dado que cada versión es acumulativa, si omite una actualización e instala la versión más reciente, seguirá teniendo acceso a todas las características y mejoras de las versiones anteriores.

Para obtener más información, consulte [Support for Current Branch versions](/sccm/core/servers/manage/current-branch-versions-supported) (Compatibilidad con las versiones de la Rama actual).

**Opciones de actualización**
- Con Software Assurance activo, puede instalar actualizaciones en la consola para las versiones de la Rama actual.  
- No hay ninguna opción para convertir la Rama actual en Technical Preview. Las versiones Technical Preview son instalaciones independientes que no requieren una licencia.
- No existe la opción de convertir la Rama actual en una Rama de mantenimiento a largo plazo (LSTB). Debe desinstalar la Rama actual y, a continuación, instalar la LTSB como una nueva instalación.

##  <a name="long-term-servicing-branch-of-system-center-configuration"></a>Rama de mantenimiento a largo plazo de System Center Configuration
Se trata de una rama con licencia para su uso en producción para los clientes de Configuration Manager que usan la Rama actual y que han permitido que su versión de Software Assurance (SA) de Configuration Manager o derechos de suscripciones equivalentes expiren después del 1 de octubre de 2016. Para obtener más información sobre Software Assurance y opciones de licencia, consulte [Licencias y ramas para System Center Configuration Manager](learn-more-editions.md).

La LTSB no recibe las actualizaciones en la consola que ofrecen nuevas características o actualizan las funciones existentes. Sin embargo, se proporcionan las revisiones de seguridad importantes.

Para instalar la LTSB como un sitio nuevo o como una actualización desde un sitio de Configuration Manager 2012 admitido, utilice los [medios de línea base](/sccm/core/servers/manage/updates#baseline-and-update-versions) de la versión 1606 que recibe en formato DVD con System Center 2016 o la versión de System Center Configuration Manager (Rama actual y Rama de mantenimiento a largo plazo 1606). Puede usar los medios de línea base para instalar un nuevo sitio que ejecuta la versión 1606 de la Rama actual o un nuevo sitio que ejecuta la Rama de mantenimiento a largo plazo.

> [!TIP]  
> Para obtener información sobre System Center 2016, consulte la [documentación de System Center 2016](https://technet.microsoft.com/system-center-docs/system-center). Esta documentación también especifica el proceso de obtención de System Center 2016, que requiere un contrato de licencia de Microsoft o derechos similares.

> Para buscar la versión 1606 de System Center Configuration Manager en el Centro de servicios de licencias por volumen (VLSC), vaya a la pestaña **Downloads and Keys (Descargas y claves)** del [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) y, después, seleccione **System Center Config Mgr (rama actual y LTSB 1606)**.

> También puede obtener una versión de evaluación de System Center 2016 en el sitio de [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).

**Características de la LTSB**
-    Recibe actualizaciones en la consola que ofrecen las revisiones de seguridad importantes
- Proporciona una opción de instalación cuando expira el contrato de SA o los derechos equivalentes para Configuration Manager
- Admite la actualización (conversión) a la Rama actual cuando tenga un contrato de SA o derechos equivalentes en vigor para Configuration Manager

**Limitaciones**  
La LTSB se basa en la versión de la Rama actual 1606 y tiene las siguientes limitaciones:
- La LTSB tiene soporte técnico durante 10 años con actualizaciones de seguridad críticas después de su disponibilidad general (octubre de 2016). Una vez transcurrido este período, el soporte para esta rama expira. Para obtener más información sobre el ciclo de vida de soporte técnico, consulte [Directiva de ciclos de vida de Microsoft](https://support.microsoft.com/en-us/lifecycle).
- Admite una lista limitada de conjuntos de sistemas operativos de servidor y cliente, y tecnologías relacionadas, como versiones de SQL Server. Para más información sobre lo que admite esta rama, consulte [Configuraciones admitidas de la rama de mantenimiento a largo plazo](supported-configurations-for-ltsb.md).
- No recibe las actualizaciones para las nuevas características.
- No admite la adición de una suscripción a Microsoft Intune, que impide el uso de:
  -    Intune en una configuración de MDM híbrida
 - MDM local
-    No admite el uso del panel de mantenimiento de Windows 10, los planes de mantenimiento, la rama actual de Windows 10 (CB) y la rama actual para empresas (CBB).
- No admite las versiones futuras de Windows 10 LTSB y Windows Server.
-    No admite Asset Intelligence.
-    No admite los puntos de distribución basados en la nube.
-    No admite Soporte técnico para Exchange Online como Exchange Connector.
-    No admite ninguna característica de versión preliminar.



**Opciones de actualización**
- Puede convertir su instalación de LTSB a una instalación de la Rama actual. Se admite la conversión a la Rama actual antes o después de que caduque la LSTB.

  Para convertir, debe tener un contrato de Software Assurance activo con Microsoft. Para obtener más información, consulte los vínculos siguientes:
  - [Upgrade the Long-Term Servicing Branch to the Current Branch](convert-to-current-branch.md) (Actualización de la Rama de mantenimiento a largo plazo a la Rama actual)
  - [Licencias y ramas para System Center Configuration Manager](learn-more-editions.md)
  - [Baseline and update versions](/sccm/core/servers/manage/updates#baseline-and-update-versions) (Versiones de línea base y actualización) en [Updates for Configuration Manager](/sccm/core/servers/manage/updates) (Actualizaciones para Configuration Manager)
- No hay ninguna opción para convertir la LTSB en Technical Preview. Las versiones Technical Preview son instalaciones independientes que no requieren una licencia.
-    No se puede actualizar una versión de evaluación de la Rama actual a una instalación de LTSB.


## <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview para System Center Configuration Manager
La versión Technical Preview está concebida para su uso en un entorno de laboratorio en el que conocer y probar las características más recientes que se están desarrollando para Configuration Manager. Technical Preview no se admite en un entorno de producción y no requiere que tenga un contrato de licencia de Software Assurance.

Para instalar un sitio nuevo que se ejecuta Technical Preview, use el [medio de línea base más reciente para System Center Configuration Manager Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Después de instalar Technical Preview, las nuevas versiones están disponibles como actualizaciones en la consola cada mes.

**Características de Technical Preview**
-  Se basa en versiones de línea base recientes de la Rama actual
-  Recibe actualizaciones en la consola que actualizan la instalación a la versión más reciente de Technical Preview
-  Incluye nuevas características que se están desarrollando y sobre las que nuestros desarrolladores querrían recibir sus comentarios
-  Recibe las actualizaciones que se aplican solo a la rama de Technical Preview

**Limitaciones**
-  [El soporte es limitado](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), por ejemplo un único sitio primario y hasta 10 clientes.  
-  No se puede actualizar a una Rama actual o LTSB.
-  No admite el uso de migración para importar o exportar datos a otra instalación de Configuration Manager.
-  No se admite la actualización desde una versión anterior de Configuration Manager.
-  No admite la instalación como una versión de evaluación.

Las características que se introducen por primera vez en una Technical Preview a menudo se agregan a la Rama actual en una actualización posterior. Cada nueva versión de Technical Preview incluye las características de las Technical Preview anteriores, incluso una vez que esas características se han agregado a la Rama actual.

Para más información, consulte [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) (Technical Preview para System Center Configuration Manager).

**Opciones de actualización**
-    Puede instalar cualquier actualización en la consola para una nueva versión de Technical Preview.
-    No hay ninguna opción para convertir una Technical Preview a la Rama actual o LTSB.

