---
title: Administrador de transferencia de paquetes | Microsoft Docs
description: "Descubra cómo el administrador de transferencia de paquetes de System Center Configuration Manager transfiere el contenido desde un servidor de sitio a los puntos de distribución remotos."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3359f254-dd48-42b7-9eab-c92a3417e3fb
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 6e61c56b9d1111287bf5a9f22832f6b1ca8146b7

---
# <a name="package-transfer-manager-in-system-center-configuration-manager"></a>Administrador de transferencia de paquetes en System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

En un sitio de System Center Configuration Manager, el administrador de transferencia de paquetes es un componente de SMS_Executive que gestiona la transferencia de contenido desde un equipo de servidor de sitio a puntos de distribución remotos en un sitio. (Un punto de distribución remoto es el que no se encuentra en el equipo de servidor del sitio). El administrador de transferencia de paquetes no es compatible con las configuraciones del administrador, pero comprender su funcionamiento puede ayudarle a planear la infraestructura de administración de contenido y a resolver problemas con la distribución de contenido.


Cuando se distribuye el contenido a uno o varios puntos de distribución remotos en un sitio, el **administrador de distribución** crea un trabajo de transferencia de contenido y después envía una notificación al administrador de transferencia de paquetes en servidores de sitio secundarios y primarios para transferir el contenido a los puntos de distribución remotos.

 El administrador de transferencia de paquetes registra sus acciones en el archivo **pkgxfermgr.log** en el servidor de sitio. El archivo de registro es la única ubicación en la que puede visualizar las actividades del administrador de transferencia de paquetes.  

> [!NOTE]  
>  En versiones anteriores de Configuration Manager, el administrador de distribución gestiona la transferencia de contenido a un punto de distribución remoto. El administrador de distribución también gestiona la transferencia de contenido entre sitios. En System Center Configuration Manager, el administrador de distribución sigue gestionando la transferencia de contenido entre dos sitios. Pero el administrador de transferencia de paquetes permite a Configuration Manager descargar del administrador de distribución las operaciones necesarias para transferir contenido a un gran número de puntos de distribución. En comparación con versiones anteriores del producto, esto permite aumentar el rendimiento general de la implementación de contenido entre los sitios y los puntos de distribución en un sitio.  

 Para transferir contenido a un punto de distribución estándar, el administrador de transferencia de paquetes funciona de la misma manera que el administrador de distribución en versiones anteriores de Configuration Manager. Es decir, administra activamente la transferencia de archivos a cada punto de distribución remoto. Sin embargo, para distribuir contenido a un punto de distribución de extracción, el administrador de transferencia de paquetes notifica al punto de distribución de extracción la disponibilidad del contenido y, a continuación, deja que el punto de distribución de extracción realice el proceso de transferencia del contenido.  

La información siguiente describe cómo el administrador de transferencia de paquetes administra la transferencia de contenido a puntos de distribución estándar y a puntos de distribución configurados como puntos de distribución de extracción:
1.  **El usuario administrativo implementa contenido en uno o varios puntos de distribución en un sitio**  

    -   **Punto de distribución estándar:** el administrador de distribución crea un trabajo de transferencia de contenido para el contenido.  

    -   **Punto de distribución de extracción:** el administrador de distribución crea un trabajo de transferencia de contenido para el contenido.  

2.  **El administrador de distribución realiza comprobaciones preliminares**  

    -   **Punto de distribución estándar:** el administrador de distribución ejecuta una comprobación básica para confirmar que cada punto de distribución está listo para recibir el contenido. Después de la comprobación, el administrador de distribución envía una notificación al administrador de transferencia de paquetes para iniciar la transferencia de contenido al punto de distribución.  

    -   **Punto de distribución de extracción:** el administrador de distribución inicia el administrador de transferencia de paquetes que luego notifica al punto de distribución de extracción la existencia de un nuevo trabajo de transferencia de contenido para el punto de distribución. El administrador de distribución no comprueba el estado de los puntos de distribución remotos que son puntos de distribución de extracción porque cada punto de distribución de extracción administra sus propias transferencias de contenido.  

3.  **El administrador de transferencia de paquetes prepara la transferencia de contenido**  

    -   **Punto de distribución estándar:** el administrador de transferencia de paquetes examina el almacén de contenido de instancia única de cada punto de distribución remoto especificado para identificar los archivos que ya están en ese punto de distribución. A continuación, el administrador de transferencia de paquetes coloca en la cola para la transferencia solo a los archivos que no están todavía presentes.  

        > [!NOTE]  
        >  Cuando se usa la acción **Redistribuir** para el contenido, el administrador de transferencia de paquetes copia cada archivo en la distribución al punto de distribución, incluso si los archivos ya figuraban en el almacenamiento de instancia única del punto de distribución.  

    -   **Punto de distribución de extracción:** para cada punto de distribución de extracción en la distribución, el administrador de transferencia de paquetes comprueba los puntos de distribución de origen de los puntos de distribución de extracción para confirmar si el contenido está disponible:  

        -   Si el contenido está disponible en, como mínimo, un punto de distribución de origen, el administrador de transferencia de paquetes envía una notificación al punto de distribución de extracción para que el punto de distribución inicie el proceso de transferencia de contenido. La notificación incluye atributos, valores hash y nombres y tamaños de archivos.  

        -   Si el contenido todavía no está disponible, el administrador de transferencia de paquetes no envía ninguna notificación al punto de distribución. En vez de ello, repetirá la comprobación cada 20 minutos hasta que el contenido esté disponible. A continuación, cuando el contenido esté disponible, el administrador de transferencia de paquetes envía la notificación al punto de distribución de extracción.  

        > [!NOTE]  
        >  Cuando se usa la acción **Redistribuir** para contenido, el punto de distribución de extracción copia cada archivo en la distribución al punto de distribución, incluso si los archivos ya figuran en el almacenamiento de instancia única del punto de distribución de extracción.  

4.  **Se inicia la transferencia de contenido**  

    -   **Punto de distribución estándar:** el administrador de transferencia de paquetes copia los archivos a cada punto de distribución remoto. Durante la transferencia a un punto de distribución estándar:  

        -   De manera predeterminada, el administrador de transferencia de paquetes puede procesar simultáneamente tres paquetes únicos y distribuirlos en cinco puntos de distribución en paralelo. Esta configuración se denomina **Configuración de distribución simultánea** y se establece en la pestaña **General** de las **Propiedades del componente de distribución de software** de cada sitio.  

        -   El administrador de transferencia de paquetes usa las configuraciones de programación y ancho de banda de red de cada punto de distribución para transferir contenido al punto de distribución correspondiente. Esta configuración se establece en las pestañas **Programación** y **Límites de frecuencia** en las **Propiedades** de cada punto de distribución remoto. Para obtener más información, vea [Administración del contenido y de la infraestructura de contenido en System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

    -   **Punto de distribución de extracción:** cuando un punto de distribución de extracción recibe un archivo de notificación, el punto de distribución empieza el proceso de transferencia de contenido. El proceso de transferencia se ejecuta de forma independiente en cada punto de distribución de extracción:  

        -   El punto de distribución de extracción identifica en la distribución de contenido los archivos que no figuran en su almacenamiento de instancia única y se prepara para descargar el contenido de uno de sus puntos de distribución de origen.  

        -   A continuación, el punto de distribución de extracción busca de forma ordenada en los puntos de distribución de origen hasta encontrar un punto de distribución de origen con el contenido disponible. Cuando el punto de distribución de extracción identifica un punto de distribución de origen con el contenido, comienza la descarga de dicho contenido.  

        > [!NOTE]  
        >  El proceso de descarga de contenido del punto de distribución de extracción es el mismo que el usado por los clientes de Configuration Manager. Para la transferencia de contenido del punto de distribución de extracción, no se utilizan ni las opciones de transferencia simultánea, ni las opciones de programación y límite que se configuran para los puntos de distribución estándar.  

5.  **La transferencia de contenido finaliza**  

    -   **Punto de distribución estándar:** cuando el administrador de transferencia de paquetes finaliza la transferencia de archivos a todos los puntos de distribución remotos, comprueba el hash del contenido en el punto de distribución y notifica al administrador de distribución la finalización de la distribución.  

    -   **Punto de distribución de extracción:** después de que el punto de distribución de extracción complete la descarga de contenido, el punto de distribución comprueba el hash del contenido y envía un mensaje de estado al punto de administración del sitio para notificar la finalización correcta del proceso. No obstante, si no se recibe el estado después de 60 minutos, el administrador de transferencia de paquetes se reactiva y comprueba el punto de distribución de extracción para confirmar que haya descargado el contenido. Si la descarga de contenido está en curso, el administrador de transferencia de paquetes se suspende durante 60 minutos antes de comprobar de nuevo el punto de distribución de extracción. Este ciclo continúa hasta que el punto de distribución de extracción completa la transferencia de contenido.  



<!--HONumber=Dec16_HO3-->


