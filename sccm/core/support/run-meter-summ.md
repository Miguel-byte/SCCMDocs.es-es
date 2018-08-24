---
title: Herramienta Run Meter Summarization
titleSuffix: Configuration Manager
description: Use la herramienta Run Meter Summarization para desencadenar las tareas de resumen de medición de software en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4815b308b1a4c93e3bc9271a3ec3af2f637b11cf
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386356"
---
# <a name="run-meter-summarization-tool"></a>Herramienta Run Meter Summarization

*Se aplica a: System Center Configuration Manager (Rama actual)*

La herramienta Run Meter Summarization es una de las [herramientas de Configuration Manager](/sccm/core/support/tools). Úsela para desencadenar inmediatamente las tareas de mantenimiento de resumen de medición de software en los sitios primarios. De forma predeterminada, estas tareas se ejecutan conforme a la programación de las tareas **Mantenimiento del sitio**, que se inician después de medianoche cada día. 

Estas tareas resumen los datos de la tabla SQL **MeterData** y escriben los resultados de resumen en las tablas **FileUsageSummary** y **MonthlyUsageSummary**. Luego el resultado resumido se ve en informes de medición de software. Cualquier usuario administrativo de Configuration Manager que pueda conectarse a la base de datos del sitio primario puede usar esta herramienta para ejecutar el resumen. 

Esta herramienta ejecuta las tareas de resumen de datos de medición de software **Resumen de uso de archivo** y **Resumen de uso mensual**. Resume todos los datos de medidor existentes sin el período de espera habitual de 12 horas. Ejecútela en la instancia de SQL Server que hospeda la base de datos del sitio. Si el resumen es correcto, el código de salida se establece en `0`. Si se ha producido un error, el código de salida es `1`.



## <a name="usage"></a>Uso

### <a name="command-line"></a>Línea de comandos

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Opciones

#### <a name="database-name"></a>Nombre de la base de datos
Nombre de la base de datos del sitio en SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Retraso del resumen en horas
La herramienta resume el uso de medición de software generado antes del retraso. De forma predeterminada, este retraso es cero.


### <a name="example"></a>Ejemplo

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Resumir el uso de medición de software generado hace 12 horas

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Consulte también

- [Tareas de mantenimiento](/sccm/core/servers/manage/maintenance-tasks)
- [Supervisar el uso de aplicaciones a través de la medición de software](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)
