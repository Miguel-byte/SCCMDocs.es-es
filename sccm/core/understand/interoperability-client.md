---
title: Usar el cliente de interoperabilidad extendida con la Rama actual | Microsoft Docs
description: "Obtenga información sobre el uso del cliente de la rama de mantenimiento a largo plazo de Configuration Manager con un sitio de rama actual."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: robstackmsft
ms.author: robstack
Robots: NOINDEX,NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 30d0177dc7fcc7f39d00c48067130d587435bf2d
ms.contentlocale: es-es
ms.lasthandoff: 12/16/2016

---
# <a name="use-the-client-software-from-the-version-1606-baseline-media-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Use el software cliente del medio de línea base de la versión 1606 para obtener una interoperabilidad extendida con futuras versiones de un sitio de rama actual.

*Se aplica a: System Center Configuration Manager (rama actual) (rama de mantenimiento a largo plazo)*  

Puede usar el software cliente de Configuration Manager para equipos con Windows (client.msi) del DVD del medio de línea base de la versión 1606 que obtiene con System Center 2016 o con una versión de System Center Configuration Manager (rama actual y rama de mantenimiento a largo plazo 1606) para administrar dispositivos que pertenecen a un sitio de rama actual. Este cliente se denomina el cliente de interoperabilidad extendida.

## <a name="how-this-scenario-works"></a>Cómo funciona este escenario:
Normalmente, cuando instala una nueva actualización en la consola de la rama actual, los clientes actualizan automáticamente su software cliente de manera que pueden usar esas características nuevas.

Con este escenario, usa la rama actual y recibe nuevas características y actualizaciones. La mayoría de los clientes ejecutan el software cliente de la rama actual y pueden actualizar ese software cliente con cada actualización de versión que instale. En cambio, en un subconjunto de sistemas críticos que no quiere que reciban actualizaciones de software cliente, instala el cliente de interoperabilidad extendida. Estos clientes no instalarán el nuevo software cliente hasta que implemente explícitamente una nueva versión del software cliente para ellos.

Más información sobre cómo evitar que los clientes de la rama actual se actualicen automáticamente cuando instale la nueva versión de Configuration Manager estará disponible con la versión 1610 de la rama actual.

El sitio de la rama actual debe ejecutar la versión 1606 o posterior.

## <a name="the-extended-interoperability-client-software"></a>El software cliente de interoperabilidad extendida
Cuando usa el cliente de interoperabilidad extendida de System Center 2016 o la versión de System Center Configuration Manager (rama actual y rama de mantenimiento a largo plazo 1606) con un sitio de rama actual, el cliente se admite durante dos años después de la disponibilidad general de la versión que es el 12 de octubre de 2016.

Planee la actualización del cliente de interoperabilidad extendida en dispositivos que administre con la rama actual antes de expire la compatibilidad con el cliente. Para hacer esto, descargue una versión nueva del cliente de Microsoft y, después, implemente ese software cliente actualizado en sus dispositivos que usen el cliente de interoperabilidad extendida actual.

**Limitaciones del cliente de interoperabilidad extendida:**
-     Las actualizaciones del software cliente de interoperabilidad extendida no están disponibles mediante las actualizaciones en la consola. Se proporcionarán detalles adicionales para la implementación de un software cliente actualizado cuando se presente un cliente actualizado.

## <a name="identify-the-client-version-you-use"></a>Identificar la versión de cliente que usa
A continuación, se muestran las versiones de cliente principales para la rama actual y la LTSB:

|Versión de cliente|Rama y versión |  
|----------------|---------------------|
|5.00.8325.xxxx |    - Rama actual 1511|
|5.00.8355.xxxx    |- Rama actual 1602|
|5.00.8412.1307    |- Rama actual 1606 </br> - Rama actual 1606 con el paquete acumulativo de revisiones 1606 (KB3186654)</br>- cliente de interoperabilidad extendida del medio de línea base de la versión 1606|  

En el cliente, puede ver la versión de cliente en la pestaña **General** del applet del panel de control de Configuration Manager.

En la pestaña **Componentes** del applet, algunos componentes muestran valores diferentes. Por ejemplo, para una versión de cliente 8412.1307, algunos componentes pueden aparecer como 5.00.8412.**1000** o 5.00.8412.**1006**.  Esta diferencia en los últimos cuatro dígitos de algunos componentes es normal y no indica un error del componente para actualizarse a la versión de cliente actual.

