---
title: Implementar actualizaciones de software | Microsoft Docs
description: "Elija las actualizaciones de software en la consola de Configuration Manager para iniciar manualmente el proceso de implementación o implementar automáticamente las actualizaciones."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
translationtype: Human Translation
ms.sourcegitcommit: e6cf8c799b5be2f7dbb6fadadddf702ec974ae45
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1

---

#  <a name="a-namebkmksumdeploya-deploy-software-updates"></a><a name="BKMK_SUMDeploy"></a> Implementar actualizaciones de software  

*Se aplica a: System Center Configuration Manager (rama actual)*

La fase de implementación de actualizaciones de software es el proceso de implementar las actualizaciones de software. Independientemente de cómo implemente las actualizaciones de software, las actualizaciones normalmente se agregan a un grupo de actualizaciones de software, estas se descargan en los puntos de distribución y el grupo de actualizaciones se implementa en los clientes. Cuando crea la implementación, se envía una directiva de actualización de software asociada a los equipos cliente y se descargan los archivos de contenido de la actualización de software desde un punto de distribución a la memoria caché local de los equipos cliente. Tras estos pasos, las actualizaciones de software están disponibles para su instalación desde el cliente. Los clientes de Internet descargan contenido desde Microsoft Update.  

> [!NOTE]  
>  Puede configurar un cliente de la intranet para que descargue actualizaciones de software desde Microsoft Update si un punto de distribución no está disponible.  

> [!NOTE]  
>  A diferencia de otros tipos de implementación, todas las actualizaciones de software se descargan en la memoria caché del cliente independientemente de la configuración de tamaño máximo de caché del cliente. Para obtener más información sobre la configuración de la memoria caché de cliente, consulte [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) (Configurar la caché del cliente para clientes de Configuration Manager).  

Si configura una implementación de actualizaciones de software requeridas, las actualizaciones de software se instalan automáticamente en la fecha límite programada. El usuario del equipo cliente puede programar o iniciar la instalación de las actualizaciones de software antes de que se cumpla la fecha límite. Tras el intento de instalación, los equipos cliente devuelven mensajes de estado al servidor de sitio para notificar si la instalación de las actualizaciones de software se completó correctamente. Para obtener más información sobre las implementaciones de actualización de software, consulte [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows) (Flujos de trabajo de implementación de actualizaciones de software).  

Hay dos escenarios principales de implementación de las actualizaciones de software: la implementación manual y la implementación automática. Normalmente, primero implementará manualmente las actualizaciones de software para crear una línea de base en los equipos cliente. A partir de ahí, administrará las actualizaciones de software mediante la implementación automática.  

## <a name="a-namebkmkmanualdeploymenta-manually-deploy-software-updates"></a><a name="BKMK_ManualDeployment"></a> Implementar actualizaciones de software manualmente
Puede seleccionar las actualizaciones de software en la consola de Configuration Manager e iniciar manualmente el proceso de implementación. Este método de implementación se utiliza normalmente para que los equipos cliente tengan todas las actualizaciones de software necesarias antes de que se creen las reglas de implementación automática que administran las implementaciones de las actualizaciones de software mensuales continuas, así como para implementar los requisitos de las actualizaciones de software fuera de banda. En la lista siguiente se indica el flujo de trabajo general de la implementación manual de las actualizaciones de software:  

1. Filtre las actualizaciones de software que utilicen requisitos específicos. Por ejemplo, podría especificar criterios para la recuperación de todas las actualizaciones de software de seguridad o imprescindibles que se requieran en más de 50 equipos cliente.  
2. Cree un grupo de actualizaciones de software que contenga las actualizaciones de software.  
3. Descargue el contenido de las actualizaciones de software en el grupo de actualizaciones de software.  
4. Implemente manualmente el grupo de actualizaciones de software.

Para obtener información detallada, consulte [Manually deploy software updates](manually-deploy-software-updates.md) (Implementar actualizaciones de software manualmente).

## <a name="automatically-deploy-software-updates"></a>Implementar actualizaciones de software automáticamente
La implementación automática de las actualizaciones de software se configura mediante una regla de implementación automática (ADR). Se trata de un método común de implementación de actualizaciones de software mensuales (lo que suele conocerse como "Patch Tuesday") y de administración de actualizaciones de definiciones. Cuando la regla se ejecuta, se quitan las actualizaciones de software del grupo de actualizaciones de software (si se está usando un grupo de actualizaciones existente); las actualizaciones de software que cumplan los criterios especificados (por ejemplo, todas las actualizaciones de software de seguridad publicadas en el último mes) se agregan a un grupo de actualizaciones de software; los archivos de contenido de las actualizaciones de software se descargan y copian en los puntos de distribución; y las actualizaciones de software se implementan en los clientes de la recopilación de destino. En la lista siguiente se indica el flujo de trabajo general para implementar automáticamente las actualizaciones de software:  

1.  Cree una ADR que especifique la configuración de implementación.
2.  Las actualizaciones de software se agregan a un grupo de actualizaciones de software.  
3.  El grupo de actualizaciones de software se implementa en los equipos cliente de la recopilación de destino (si se ha especificado).  

Debe determinar la estrategia de implementación que se utilizará en su entorno. Por ejemplo, podría crear la ADR y seleccionar una recopilación de destino de clientes de prueba. Después de comprobar que las actualizaciones de software estén instaladas en el grupo de prueba, puede agregar una nueva implementación a la regla o cambiar la recopilación de la implementación existente por una recopilación de destino que incluya un conjunto de clientes más amplio. Los objetos de actualización de software que se crean mediante reglas ADR son interactivos.  

-   Las actualizaciones de software que se implementaron mediante una ADR se implementan automáticamente en los nuevos clientes agregados a la recopilación de destino.  
-   Las nuevas actualizaciones de software que se agregan a un grupo de actualizaciones de software se implementan automáticamente en los clientes de la recopilación de destino.  
-   Puede habilitar o deshabilitar las implementaciones en cualquier momento para la ADR.  

Después de crear una ADR, puede agregar implementaciones adicionales a la regla. Esto puede ayudarle a administrar la complejidad de la implementación de varias actualizaciones en diferentes recopilaciones. Cada nueva implementación ofrece todas las funcionalidades y la experiencia completa de supervisión de la implementación, y todas las implementaciones nuevas que agrega:  

-   Usan el mismo grupo y paquete de actualizaciones que se creó la primera vez que se ejecutó el ADR.  
-   Pueden especificar una recopilación diferente.  
-   Admiten propiedades de implementación únicas, como:  
   -   Hora de activación  
   -   Fecha límite  
   -   Mostrar u ocultar la experiencia del usuario final  
   -   Alertas independientes para esta implementación  

Para obtener información detallada, consulte [Automatically deploy software updates](automatically-deploy-software-updates.md) (Implementar actualizaciones de software automáticamente).

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->



<!--HONumber=Dec16_HO3-->


