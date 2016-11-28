---
title: "Procedimientos recomendados para la generación de informes | System Center Configuration Manager"
description: "Lea algunas sugerencias de utilidad sobre el uso de la capacidad de generación de informes de System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fae72b0455b53923aaf93b5b53afb562bedc2eca


---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Procedimientos recomendados para la generación de informes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use los procedimientos recomendados siguientes para la generación de informes en System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Para un rendimiento óptimo, instale el punto de servicios de informes en un servidor de sistema de sitio remoto  
 Aunque puede instalar el punto de servicios de informes en un servidor de sitio o en un sistema de sitio remoto, el rendimiento aumenta cuando lo instala en un servidor de sistema de sitio remoto.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Optimizar consultas de SQL Server Reporting Services  
 Normalmente, los retrasos de los informes se deben al tiempo que se tarda en ejecutar consultas y recuperar los resultados. Si está utilizando Microsoft SQL Server, herramientas como el analizador de consultas y el generador de perfiles pueden ayudarle a optimizar las consultas.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Programar el procesamiento de la suscripción de informes para que se ejecute fuera del horario de oficina estándar  
 Siempre que sea posible, programe el procesamiento de suscripción de informes para que se ejecute fuera del horario de oficina normal a fin de minimizar el procesamiento de la CPU en el servidor de base de datos de sitio de Configuration Manager. Esta práctica también mejora la disponibilidad de solicitudes de informes imprevistas.  

## <a name="next-steps"></a>Pasos siguientes
[Configurar la generación de informes](configuring-reporting.md)



<!--HONumber=Nov16_HO1-->


