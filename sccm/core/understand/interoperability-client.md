---
title: 'Uso del cliente de interoperabilidad extendida con la Rama actual '
titleSuffix: Configuration Manager
description: "Obtenga información sobre el uso del cliente de la rama de mantenimiento a largo plazo de Configuration Manager con un sitio de rama actual."
ms.custom: na
ms.date: 08/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: ba79f2b9cf0cdfc4525645a647dddb624a0a5e5b
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2017
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Uso del software cliente de Configuration Manager para obtener una interoperabilidad extendida con futuras versiones de un sitio de la Rama actual

*Se aplica a: System Center Configuration Manager (Rama actual), (Rama de mantenimiento a largo plazo)*  

En algunos casos, las directivas de la empresa podría no permitir realizar actualizaciones regulares del cliente de Configuration Manager en algunos equipos. Por ejemplo, es posible que deba cumplir con las directivas de administración de cambios, o el dispositivo puede ser crítico.

Aunque debe seguir utilizando la actualización automática para la mayoría de los clientes, cuando sea posible, a partir de la actualización 1610 de Configuration Manager, puede satisfacer estas necesidades con la instalación de un cliente nuevo para un uso a largo plazo, denominado cliente de interoperabilidad extendida.

El EIC es compatible con sitios de Configuration Manager que ejecutan la versión 1610 o posterior. El EIC solo debe usarse para equipos específicos que no se puede actualizar con frecuencia, como los dispositivos de pantalla completa o de punto de venta. Utilice al cliente de Configuration Manager más reciente para todos los demás equipos.

## <a name="how-this-scenario-works"></a>Cómo funciona este escenario

Normalmente, cuando instala una nueva actualización en la consola de la rama actual, los clientes actualizan automáticamente su software cliente de manera que pueden usar esas características nuevas.

Con este escenario, usa la rama actual y recibe nuevas características y actualizaciones. La mayoría de los clientes ejecutan el software cliente de la rama actual y pueden actualizar ese software cliente con cada actualización de versión que instale. En cambio, en un subconjunto de sistemas críticos que no quiere que reciban actualizaciones de software cliente, instala el cliente de interoperabilidad extendida. Estos clientes no instalan el nuevo software cliente hasta que implemente explícitamente una nueva versión del software cliente para ellos.

>[!IMPORTANT]
>El sitio de la Rama actual debe ejecutar la versión 1610 o posterior.

## <a name="how-to-use-the-eic"></a>Cómo usar el EIC

1. Obtenga el EIC (versión de cliente 5.00.8412) de la carpeta \SMSSETUP\Client del medio de instalación de la actualización 1606 de Configuration Manager. Asegúrese de copiar todo el contenido de la carpeta.
2. Instale manualmente el EIC en dichos dispositivos. [Lea más información sobre cómo instalar manualmente el cliente](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).
3. Excluya esa colección de las actualizaciones de cliente.

>[!TIP]
>Para buscar la versión 1606 de System Center Configuration Manager en el Centro de servicios de licencias por volumen (VLSC), vaya a la pestaña **Downloads and Keys** (Descargas y claves) de [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) y, después, seleccione **System Center Config Mgr (rama actual y LTSB)**.

## <a name="the-extended-interoperability-client-software"></a>El software cliente de interoperabilidad extendida

El EIC actual seguirá siendo compatible con las versiones actualizadas de la Rama actual de Configuration Manager al menos hasta el 18 de noviembre de 2018. Transcurrido ese tiempo, consulte esta página para obtener información sobre un nuevo EIC o una extensión de compatibilidad del EIC existente.

>[!TIP]
>Se admite el EIC durante al menos dos años desde la fecha de lanzamiento (vea [Compatibilidad con versiones de la rama actual de System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)). Por ejemplo, el EIC actual seguirá siendo compatible durante dos años después del lanzamiento de la actualización 1610, que es el 18 de noviembre de 2018.

Planee la actualización del cliente de interoperabilidad extendida en dispositivos que administre con la rama actual antes de expire la compatibilidad con el cliente. Para ello, descargue una versión nueva del cliente de Microsoft y, después, implemente ese software cliente actualizado en sus dispositivos que usen el cliente de interoperabilidad extendida actual.

## <a name="limitations-of-the-extended-interoperability-client"></a>Limitaciones del cliente de interoperabilidad extendida

- Las actualizaciones del software cliente de interoperabilidad extendida no están disponibles mediante las actualizaciones en la consola. Se proporcionan detalles adicionales para la implementación de un software cliente actualizado cuando se presente un cliente actualizado.
- El EIC solo es compatible con las actualizaciones de software, inventario y paquetes y programas.

## <a name="next-steps"></a>Pasos siguientes

Lea la información sobre [supervisión de clientes](/sccm/core/clients/manage/monitor-clients) para asegurarse de que los clientes están instalados correctamente en los dispositivos que desea.
