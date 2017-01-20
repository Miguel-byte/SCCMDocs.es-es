---
title: Simular implementaciones de aplicaciones | System Center Configuration Manager
description: "Evalúe el método de detección, los requisitos y las dependencias de un tipo de implementación sin instalar la aplicación."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simular implementaciones de aplicaciones con System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Si desea probar la aplicabilidad de una implementación de aplicaciones en equipos sin instalar o desinstalar la aplicación, use implementaciones simuladas. Una implementación simulada evalúa el método de detección, los requisitos y las dependencias de un tipo de implementación y muestra los resultados en el nodo **Implementaciones** del área de trabajo **Supervisión** . Use el procedimiento de este tema para simular una implementación de aplicación en System Center Configuration Manager.  

> [!NOTE]  
>  No puede usar implementaciones simuladas para recopilaciones de dispositivos móviles.  
>   
>  No puede implementar una aplicación con un propósito de implementación **Desinstalar** si se activó una implementación simulada de la misma aplicación.  
  
Use el siguiente procedimiento para configurar una implementación de aplicación simulada:
  
1.  En la consola de Configuration Manager, seleccione uno de los siguientes:  

    -   Una recopilación de usuarios.  

    -   Una recopilación de dispositivos.  

    -   Una aplicación de Configuration Manager.  

2.  En la pestaña **Inicio** , en el grupo **Implementación** , haga clic en **Simular implementación**.  

3.  En **Asistente para simular implementación de aplicaciones**, especifique la siguiente información:  

    -   **Aplicación** : haga clic en **Examinar** y, a continuación, seleccione la aplicación para la que quiere crear una implementación simulada.  

    -   **Recopilación** : haga clic en **Examinar** y, a continuación, seleccione la recopilación que quiere usar para la implementación simulada.  

    -   **Acción** : en la lista desplegable, seleccione si quiere simular la instalación o la desinstalación de la aplicación seleccionada.  

    -   **Implementar automáticamente con o sin inicio de sesión del usuario** : si se activa esta opción, los clientes evaluarán la implementación simulada independientemente de si los clientes han iniciado sesión.  

4.  Haga clic en **Siguiente**, revise la información en la página **Resumen** y, a continuación, complete el asistente para crear la implementación simulada.  

5.  Las aplicaciones simuladas aparecen en el nodo **Implementaciones** del área de trabajo **Supervisión** con el propósito **Simular**. Para obtener más información sobre cómo supervisar implementaciones de aplicaciones, consulte [Supervisar aplicaciones desde la consola de System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  



<!--HONumber=Nov16_HO1-->


