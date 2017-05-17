---
title: "Elegir Intune independiente o MDM híbrida | Microsoft Docs"
description: "Elija si quiere implementar la administración de dispositivos móviles híbrida con Intune y Configuration Manager o ejecutar Intune de forma independiente."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.contentlocale: es-es
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Elegir entre Microsoft Intune independiente y administración de dispositivos móviles híbrida con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Una de las preguntas más frecuentes relacionadas con la administración de dispositivos móviles (MDM) con Microsoft Intune es "¿Debo integrar Intune con Configuration Manager (MDM híbrida) o ejecutar Intune independiente en la configuración de solo en la nube?". Para responder esa pregunta, debe comparar las dos opciones con atención y tener en cuenta las actualizaciones de principios de 2017 para Intune independiente.

## <a name="what-is-intune-standalone"></a>¿Qué es Intune independiente?

Intune independiente es una solución de MDM solo en la nube que no implica recursos locales y que se administra mediante una consola web a la que se puede acceder desde cualquier lugar del mundo. Los centros de datos de Intune se hospedan en Norteamérica, Europa y Asia. Como Intune es un servicio en la nube, puede implementar la administración de Intune en sus dispositivos en un período de tiempo relativamente corto. También puede optar por Intune independiente si su organización se está moviendo a la nube.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>¿Qué es MDM híbrida con Configuration Manager?

MDM híbrida es una solución que usa Intune como el canal de entrega de directivas, perfiles y aplicaciones a los dispositivos, pero usa infraestructura local de Configuration Manager para almacenar y administrar contenido y administrar los dispositivos. Puede elegir MDM híbrida si ya tiene una inversión importante en Configuration Manager y quiere ampliarla para administrar dispositivos móviles. Una implementación híbrida le proporciona un control "desde una única ubicación", lo que significa que puede usar la misma infraestructura local y consola administrativa para administrar dispositivos móviles con Intune así como equipos y servidores con el cliente tradicional de Configuration Manager.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Novedades de Intune independiente a principios de 2017

Si está decidiendo entre independiente e híbrido, debe tener en cuenta las características que llegarán a principios de 2017 para Intune independiente. Hoy en día, MDM híbrida tiene varias características avanzadas que históricamente han sido la razón de que muchos clientes decidan administrar sus dispositivos con MDM híbrida en lugar de con Intune independiente:

-   Acceso mediante programación (API): opciones de administración de PowerShell y SDK.

-   Generación de informes personalizados: crear informes personalizados.

-   Control de acceso basado en roles: restringir el acceso a funciones administrativas en función de los roles asignados.

-   Escalar: implementar y administrar más de 100 000 dispositivos móviles.

-   Única ubicación: administrar clientes PC tradicionales y dispositivos administrados en Intune con la misma consola.

Si está comenzando a planear su implementación a Intune hoy y tiene un período de varios meses para pruebas piloto, pruebas de aceptación e implementación, considere la posibilidad de elegir Intune independiente ahora conociendo las actualizaciones que llegarán al servicio en la nube y que incluirán más características. A lo largo de la primera mitad del año natural 2017, Intune independiente recibirá actualizaciones que proporcionan gran parte de las características avanzadas de una implementación híbrida con Configuration Manager. Intune independiente se moverá pronto a la plataforma en la nube de Microsoft Azure y con esta tendrá una escalabilidad mejorada, un acceso basado en roles mediante Azure Portal, informes personalizados y un acceso mediante programación con API Graph de Azure.

Puede cambiar de híbrido a Intune independiente o viceversa, pero requiere ayuda del soporte técnico de Microsoft y del equipo de operaciones. También requiere anular la inscripción y volver a inscribir posteriormente todos los dispositivos después de que se cambie la entidad de administración.  Microsoft está trabajando para mejorar la experiencia de cambiar configuraciones en una actualización de servicio futura.

