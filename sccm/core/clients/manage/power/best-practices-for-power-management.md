---
title: Procedimientos recomendados para la administración de energía
titleSuffix: Configuration Manager
description: Conozca procedimientos recomendados para la administración de energía en System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 480f7a890e82b46e2b2d69180763f39504a47e0c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344490"
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Procedimientos recomendados para la administración de energía en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

Use los procedimientos recomendados siguientes para la administración de energía en System Center Configuration Manager.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Realizar la fase de supervisión en un momento representativo  
 La fase de supervisión de la administración de energía le ofrece información sobre el consumo de energía, la actividad, las capacidades de administración de energía y del impacto medioambiental de los equipos de su organización. Asegúrese de elegir una hora representativa para realizar la fase de supervisión. Por ejemplo, si realiza la fase de supervisión en un día festivo, no obtendrá un informe realista sobre el uso de energía del equipo.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Crear una recopilación de controles de equipos sin planes de energía aplicados  
 Cree dos recopilaciones de equipos para ayudarle a supervisar los efectos de la aplicación de los planes de energía en equipos. La primera recopilación debe contener la mayoría de los equipos en los que quiere aplicar la configuración de energía y la otra recopilación (la recopilación de controles) debe contener el resto de equipos. Aplique el plan de administración de energía necesario para la recopilación que contenga la mayoría de los equipos. Después, puede ejecutar informes para comparar el costo de energía, el uso de energía y el impacto medioambiental de los equipos en los que ha aplicado la configuración de energía, con la recopilación de controles en la que no ha aplicado la configuración de energía.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Ejecutar el informe de configuración de energía antes de aplicar un plan de administración de energía  
 Antes de aplicar un plan de administración de energía a un conjunto de equipos, ejecute el informe **Configuración de energía** , el cual le ayudará a comprender la configuración de administración de energía que ya está configurada en los equipos de la recopilación. Si aplica la nueva configuración de administración de energía en equipos sin examinar primero la configuración existente, puede provocar un aumento del consumo de energía.  

## <a name="exclude-servers-from-power-management"></a>Excluir los servidores de la administración de energía  
 No se admite la administración de energía en equipos que ejecuten Windows Server (aunque se recopilen datos de uso de energía). Asegúrese de agregar servidores a una recopilación y exclúyala de la administración de energía.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Excluir equipos que no quiere administrar  
 Si tiene equipos que no quiere administrar con administración de energía, agréguelos a una recopilación y asegúrese de que la recopilación se excluye de la administración de energía.  

 Entre los ejemplos de equipos que podría querer excluir de la administración de energía se incluyen:  

-   Los equipos que deban permanecer encendidos.  

-   Los equipos a los que los usuarios deban conectarse mediante Conexión a Escritorio remoto.  

-   Los equipos que no puedan utilizar la administración de energía.  

-   Los equipos que tengan el rol de sistema de sitio de punto de distribución.  

-   Los equipos públicos como los quioscos multimedia, las pantallas de información o las consolas de supervisión, donde el equipo y el monitor siempre deben estar encendidos.  

 Para más información, vea [Configuración de administración de energía en Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>En primer lugar, aplique los planes de energía a un recopilación de equipos de prueba  
 Pruebe siempre el efecto de aplicar un plan de administración de energía en un conjunto de equipos de prueba antes de aplicar el plan de energía a un gran conjunto de equipos.  

 La configuración de energía que se aplica a los equipos que ejecutan Windows XP o Windows Server 2003 no se revierte a su valor original, ni aunque excluya el equipo de la administración de energía. En versiones posteriores de Windows, la exclusión de un equipo de la administración de energía hace que toda la configuración de energía revierta a sus valores originales. No puede revertir una configuración de energía individual a sus valores originales.  

## <a name="apply-power-plan-settings-individually"></a>Aplicar la configuración de plan de energía individualmente  
 Supervise el efecto de aplicar cada configuración de energía antes de aplicar la siguiente para asegurarse de que cada valor tenga el efecto necesario. Para más información sobre la configuración del plan de energía, vea [Configuración de Plan de administración de energía disponibles](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) en el tema [Cómo crear y aplicar energía planes en Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Supervisar periódicamente los equipos para ver si tienen varios planes de energía aplicados  
 La administración de energía incluye un informe en el que se muestran los equipos que tengan varios planes de energía aplicados.  

 Si un equipo es miembro de varias recopilaciones y cada una de ellas aplica planes de energía diferentes, se realizará las siguientes acciones:  

-   Plan de energía: si se aplican varios valores para la configuración de energía en un equipo, se usa el valor menos restrictivo.  

-   Hora de reactivación: si se aplican varias horas de activación a un equipo de escritorio, se usará la hora más cercana a medianoche.  

     Para más información, vea [Equipos con varios planes de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) en el tema [Cómo supervisar y planear la administración en el Administrador de configuración de energía](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). Para más información sobre cómo resuelve los conflictos la administración de energía, vea [Cómo crear y aplicar energía planes en Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Guardar o exportar información de la administración de energía durante la fase de supervisión y planificación de la administración de energía  
 La información de administración de energía usada en los informes diarios se conserva en la base de datos de sitio de Configuration Manager durante 31 días.  

 La información de administración de energía usada en los informes mensuales se conserva en la base de datos de sitio de Configuration Manager durante 13 meses.  

 Cuando ejecute informes durante las fases de supervisión, planeamiento y cumplimiento de la administración de energía, guarde o exporte los resultados de aquellos cuyos datos quiera conservar para una comparación posterior por si Configuration Manager los elimina más adelante.  
