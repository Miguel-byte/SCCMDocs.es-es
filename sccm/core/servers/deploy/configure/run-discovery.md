---
title: "Ejecutar la detección | System Center Configuration Manager"
description: "Lea la información general sobre el proceso de detección y los registros de datos de detección."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 30844519-ce14-456f-bfb8-4318b578e9f6
caps.latest.revision: 20
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d73b493318b0a1938d42265ec03369015365addb


---
# <a name="run-discovery-for-system-center-configuration-manager"></a>Ejecutar la detección para System Center Configuration Manager

*Se aplica a: System Center Configuration Manager (rama actual)*

Use uno o varios métodos de detección en    
      System Center Configuration Manager para buscar recursos de dispositivo y de usuario que se pueden administrar. También puede usar la detección para identificar la infraestructura de red en su entorno.  Existen varios métodos de detección diferentes que puede usar para detectar cosas diferentes, y cada método tiene su propia configuración y limitaciones.  

## <a name="overview-of-discovery"></a>Información general sobre la detección  
 La detección es el proceso mediante el cual Configuration Manager conoce los elementos que puede administrar. Estos son los métodos de detección disponibles:  

-   Detección de bosques de Active Directory  

-   Detección de grupos de Active Directory  

-   Detección de sistemas de Active Directory  

-   Detección de usuario de Active Directory  

-   Detección de latidos  

-   Detección de redes  

-   detección de servidores  

> [!TIP]  
>  Encontrará más información sobre los métodos de detección individuales en [Acerca de los métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  
>   
>  Para obtener ayuda para seleccionar los métodos que va a usar y en qué sitios de la jerarquía, consulte [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md) (Selección de los métodos de detección que se usarán para System Center Configuration Manager).  

 Para usar la mayoría de los métodos de detección, debe habilitar el método en un sitio y configurarlo para buscar ubicaciones específicas de red o de Active Directory. Cuando se ejecuta, consulta en la ubicación especificada información sobre los dispositivos o usuarios que Configuration Manager puede administrar.  Cuando un método de detección encuentra correctamente información sobre un recurso, coloca dicha información en un archivo denominado registro de datos de detección (DDR), que se procesa mediante un sitio de administración central o primario. El procesamiento de un DDR crea un nuevo registro en la base de datos del sitio para los recursos recién detectados, o bien actualiza los registros existentes con la información nueva.  

 Algunos métodos de detección pueden generar un gran volumen de tráfico de red y los DDR resultantes pueden dar lugar a un uso significativo de recursos de CPU durante el procesamiento. Por lo tanto, considere usar solamente aquellos métodos de detección que vayan a cumplir sus objetivos. Podría comenzar usando solo uno o dos métodos de detección y luego más tarde habilitar métodos adicionales de una manera controlada para ampliar el nivel de detección en su entorno.  

 Después de que la información de detección se agrega a la base de datos del sitio, se replica en cada sitio de la jerarquía, con independencia del sitio en el que se detectara o procesara. Por lo tanto, aunque puede configurar distintas programaciones y métodos de detección en diferentes sitios, un método de detección específico solo se puede ejecutar en un sitio para reducir el uso de ancho de banda de red mediante acciones de detección duplicadas y disminuir el procesamiento de datos de detección redundantes en múltiples sitios.  

 Puede usar los datos de detección para crear colecciones y consultas personalizadas que agrupen lógicamente los recursos para tareas de administración como las siguientes:  

-   Insertar instalaciones de cliente o actualizar  

-   Implementar el contenido en usuarios o dispositivos  

-   Implementar la configuración de cliente y las configuraciones relacionadas  

##  <a name="a-namebkmkddrsa-about-discovery-data-records"></a><a name="BKMK_DDRs"></a> Acerca de los registros de datos de detección  
 Los registros de datos de detección (DDR) son archivos creados por un método de detección que contienen información sobre los recursos que se pueden administrar en Configuration Manager. Los DDR contienen información acerca de los equipos, los usuarios y, en algunos casos, la infraestructura de red. Estos se procesan en sitios primarios o en sitios de administración central. Después de que la información sobre los recursos del DDR se incluye en la base de datos, se elimina el DDR y se replica la información como datos globales en todos los sitios de la jerarquía.  

 El sitio en que se procesa un DDR depende de la información que contiene:  

-   Los DDR de los nuevos recursos detectados que no se encuentran en la base de datos se procesan en el sitio de primer nivel de la jerarquía. El sitio de primer nivel crea un nuevo registro de recursos en la base de datos y le asigna un identificador único. Los DDR se transfieren mediante la replicación basada en archivos hasta que alcanzan el sitio de primer nivel.  

-   Los DDR de los objetos detectados anteriormente se procesan en sitios primarios. Los sitios primarios secundarios no transfieren DDR al sitio de administración central cuando el DDR contiene información sobre un recurso que ya está en la base de datos.  

-   Los sitios secundarios no procesan los registros de datos de detección y siempre los transfieren a su sitio primario principal mediante la replicación basada en archivos.  

Los archivos DDR se identifican por la extensión .ddr y tienen un tamaño típico de aproximadamente 1 kB.  

## <a name="get-started-with-discovery"></a>Introducción a la detección:  
 Antes de utilizar la consola de Configuration Manager para configurar la detección, debe entender las diferencias entre los métodos, qué hacen y, en el caso de algunos, sus limitaciones.  
Los siguientes temas pueden servir como base para ayudarle a usar los métodos de detección satisfactoriamente:  

-   [Acerca de los métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md)  

-   [Select discovery methods to use for System Center Configuration Manager](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md) (Selección de los métodos de detección que se usarán para System Center Configuration Manager)  

Después, cuando sepa qué métodos desea usar, busque información para configurar cada método en [Configurar métodos de detección para System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  



<!--HONumber=Nov16_HO1-->


