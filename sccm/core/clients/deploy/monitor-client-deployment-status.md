---
title: "Supervisar el estado de implementación de cliente | Microsoft Docs"
description: "Supervise el estado de implementación de cliente en System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 20a573b3-53cb-4ed5-bae1-7542f533ed20
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 52d2e088b8db3c2e9a0af640ca3db72b9fd7af60
ms.openlocfilehash: 0ca218e4276699dd9029308e1d8ac524563da7c5
ms.lasthandoff: 01/03/2017


---
# <a name="how-to-monitor-client-deployment-status-in-system-center-configuration-manager"></a>Supervisar el estado de implementación de cliente en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (Rama actual)*

La implementación de clientes en el sitio lleva tiempo y algunas instalaciones no se realizan correctamente la primera vez. La consola de System Center Configuration Manager ofrece una manera de vigilar las implementaciones de cliente en una recopilación mediante la notificación de su estado en tiempo real.  

> [!NOTE]  
>  La manera mejor y más confiable de supervisar la implementación del cliente es con la consola de Configuration Manager (como se describe en este artículo). La sección **Estado de cliente** del área de trabajo **Supervisión** de la consola proporciona información precisa y en tiempo real sobre el estado de la implementación. Las implementaciones de cliente se pueden supervisar con otras herramientas, como el Administrador de servidores de Windows Server o System Center Operations Manager, pero puede recibir alarmas aunque la actividad de la instalación de cliente sea normal. Como el programa de instalación de cliente (CCMSetup.exe) se ejecuta en varios entornos, estas otras herramientas pueden generar falsas alarmas y advertencias que no reflejan con precisión el estado de las implementaciones de cliente.  

 En el área de trabajo **Supervisión** de la consola, puede supervisar los siguientes estados para las implementaciones de cliente que tienen lugar dentro de una recopilación especificada:  

-   conforme  

-   En curso  

-   No conforme  

-   Error  

-   Desconocida  

 Informes de Configuration Manager en implementaciones de clientes de producción o clientes de preproducción. La consola de Configuration Manager también proporciona un gráfico de implementaciones de cliente erróneas durante un período de tiempo especificado para ayudarle a determinar si las acciones que realiza para solucionar los problemas con las implementaciones mejoran su índice de éxito con el tiempo.  

## <a name="to-monitor-client-deployments"></a>Para supervisar las implementaciones de cliente  

-   En la consola de Configuration Manager, haga clic en **Supervisión** > **Estado de cliente**.  

-   Haga clic en **Implementación del cliente de producción** o **Implementación del cliente de preproducción**, según la versión de cliente que quiera supervisar.  

-   Revise los gráficos de estado de implementación de cliente y error de implementación de cliente.  

-   Si quiere cambiar el ámbito del informe, haga clic en **Examinar...** y elija otra recopilación.  

 Para más información sobre las implementaciones de cliente de preproducción, vea [Cómo probar las actualizaciones de cliente en una recopilación de preproducción en System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).

 > [!NOTE]
 > El estado de implementación en equipos que hospedan los roles de sistema de sitio en una recopilación de preproducción puede aparecer registrado como **No compatible** incluso cuando el cliente se ha implementado correctamente. Cuando se promueve el cliente a la producción, el estado de implementación se registrará correctamente.   

 Para supervisar el estado de los clientes implementados, consulte [Supervisar clientes en System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

 Puede usar informes de Configuration Manager para tener más información sobre el estado de los clientes en el sitio. Para más información sobre cómo ejecutar informes, consulte [Generación de informes en System Center Configuration Manager](../../../core/servers/manage/reporting.md).  

